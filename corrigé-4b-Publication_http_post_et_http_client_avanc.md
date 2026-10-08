# Correction TP 2 : Envoi de Données HTTP POST et En-têtes Personnalisés en Go

## Solution complète (`main.go`)

```go
package main

import (
	"bytes"
	"encoding/json"
	"fmt"
	"io"
	"log"
	"net/http"
)

// Article représente la structure à envoyer et à recevoir
type Article struct {
	ID     int    `json:"id,omitempty"` // omitempty permet de ne pas envoyer "id": 0 lors du POST
	Title  string `json:"title"`
	Body   string `json:"body"`
	UserID int    `json:"userId"`
}

func main() {
	targetURL := "https://jsonplaceholder.typicode.com/posts"

	// Étape 1 : Création et sérialisation de l'objet
	newArticle := Article{
		Title:  "Introduction aux API en Go",
		Body:   "Le package net/http permet de créer des clients performants.",
		UserID: 42,
	}

	jsonData, err := json.Marshal(newArticle)
	if err != nil {
		log.Fatalf("Erreur lors du marshalling JSON : %v", err)
	}

	fmt.Println("=== 1. JSON généré ===")
	fmt.Println(string(jsonData))
	fmt.Println()

	// Étape 2 : Démonstration rapide avec http.Post (pour comparaison)
	fmt.Println("=== 2. Envoi simplificatif via http.Post ===")
	respSimple, err := http.Post(targetURL, "application/json", bytes.NewBuffer(jsonData))
	if err != nil {
		log.Fatalf("Erreur http.Post : %v", err)
	}
	defer respSimple.Body.Close()
	fmt.Printf("Statut http.Post : %s (Code: %d)\n\n", respSimple.Status, respSimple.StatusCode)

	// Étape 3 : Implémentation avancée avec http.Client et headers
	fmt.Println("=== 3. Envoi avancé avec http.Client & Headers ===")
	
	// Création de la requête HTTP POST
	req, err := http.NewRequest("POST", targetURL, bytes.NewBuffer(jsonData))
	if err != nil {
		log.Fatalf("Erreur lors de la création de la requête : %v", err)
	}

	// Configuration des en-têtes (Headers)
	req.Header.Set("Content-Type", "application/json; charset=UTF-8")
	req.Header.Set("Authorization", "Bearer my_secret_token_12345")

	// Instanciation du client et exécution
	client := &http.Client{}
	resp, err := client.Do(req)
	if err != nil {
		log.Fatalf("Erreur lors de l'exécution de la requête : %v", err)
	}
	defer resp.Body.Close()

	fmt.Printf("Statut réponse : %s (Code: %d)\n", resp.Status, resp.StatusCode)

	// Vérification du code HTTP 201 Created
	if resp.StatusCode != http.StatusCreated && resp.StatusCode != http.StatusOK {
		log.Fatalf("Échec de la création, code reçu : %d", resp.StatusCode)
	}

	// Étape Challenge : Décodage de la réponse serveur
	body, err := io.ReadAll(resp.Body)
	if err != nil {
		log.Fatalf("Erreur de lecture du corps : %v", err)
	}

	var createdArticle Article
	if err := json.Unmarshal(body, &createdArticle); err != nil {
		log.Fatalf("Erreur de désérialisation de la réponse : %v", err)
	}

	fmt.Println("\n=== Challenge : Article créé retourné par le serveur ===")
	fmt.Printf("ID attribué : %d\n", createdArticle.ID)
	fmt.Printf("Titre       : %s\n", createdArticle.Title)
	fmt.Printf("UserID      : %d\n", createdArticle.UserID)
}
```

---

## Explications pédagogiques et erreurs fréquentes

1. **Conversion du JSON en flux (`bytes.NewBuffer`) :**
   - `http.Post` et `http.NewRequest` attendent un type respectant l'interface `io.Reader`. `json.Marshal` fournissant un `[]byte`, l'utilisation de `bytes.NewBuffer(jsonData)` ou `bytes.NewReader(jsonData)` est obligatoire.

2. **Tag `omitempty` :**
   - Expliquer aux étudiants l'importance de `json:"id,omitempty"`. Lors de l'envoi d'un nouvel objet, l'ID n'est pas encore défini (valeur zéro par défaut en Go : `0`). Le tag empêche l'envoi du champ `"id": 0` au serveur.

3. **Différence `http.Post` vs `http.Client.Do` :**
   - Rappeler aux apprenants que `http.Post` est un *wrapper* pratique mais limité. Dès qu'un header d'authentification (comme `Authorization`), de paramètre personnalisé ou de délai d'attente (*timeout*) est nécessaire, l'usage de `http.Client` avec `http.NewRequest` devient indispensable.