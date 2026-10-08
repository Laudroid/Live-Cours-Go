# Correction TP 4a : Consommation d'une API REST GET et Décodage JSON en Go

## Solution complète (`main.go`)

```go
package main

import (
	"encoding/json"
	"fmt"
	"io"
	"log"
	"net/http"
)

// Todo représente la structure d'une tâche renvoyée par l'API
type Todo struct {
	UserID    int    `json:"userId"`
	ID        int    `json:"id"`
	Title     string `json:"title"`
	Completed bool   `json:"completed"`
}

// getTodoByID récupère une seule tâche en fonction de son ID (Étape 2)
func getTodoByID(id int) (*Todo, error) {
	url := fmt.Sprintf("https://jsonplaceholder.typicode.com/todos/%d", id)

	// Envoi de la requête GET
	resp, err := http.Get(url)
	if err != nil {
		return nil, fmt.Errorf("erreur lors de la requête HTTP : %w", err)
	}
	// Toujours fermer le corps de réponse pour libérer les connexions TCP
	defer resp.Body.Close()

	// Challenge : Vérification des codes de statut HTTP
	if resp.StatusCode == http.StatusNotFound {
		return nil, fmt.Errorf("tâche non trouvée (Code 404)")
	}
	if resp.StatusCode != http.StatusOK {
		return nil, fmt.Errorf("statut HTTP inattendu : %s", resp.Status)
	}

	// Lecture du corps de la réponse
	body, err := io.ReadAll(resp.Body)
	if err != nil {
		return nil, fmt.Errorf("erreur de lecture du corps : %w", err)
	}

	// Décodage JSON vers la structure Todo
	var todo Todo
	if err := json.Unmarshal(body, &todo); err != nil {
		return nil, fmt.Errorf("erreur de décodage JSON : %w", err)
	}

	return &todo, nil
}

// getTodosByUser récupère toutes les tâches d'un utilisateur spécifique (Étape 3)
func getTodosByUser(userID int) ([]Todo, error) {
	url := fmt.Sprintf("https://jsonplaceholder.typicode.com/todos?userId=%d", userID)

	resp, err := http.Get(url)
	if err != nil {
		return nil, fmt.Errorf("erreur lors de la requête HTTP : %w", err)
	}
	defer resp.Body.Close()

	if resp.StatusCode != http.StatusOK {
		return nil, fmt.Errorf("statut HTTP inattendu : %s", resp.Status)
	}

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		return nil, fmt.Errorf("erreur de lecture du corps : %w", err)
	}

	// Décodage du tableau JSON vers une slice de Todo ([]Todo)
	var todos []Todo
	if err := json.Unmarshal(body, &todos); err != nil {
		return nil, fmt.Errorf("erreur de décodage JSON : %w", err)
	}

	return todos, nil
}

func main() {
	fmt.Println("=== 1. Récupération d'un Todo unique (ID = 1) ===")
	todo, err := getTodoByID(1)
	if err != nil {
		log.Fatalf("Erreur : %v", err)
	}
	fmt.Printf("Todo récupéré : ID=%d, Titre=\"%s\", Complété=%t\n\n", todo.ID, todo.Title, todo.Completed)

	fmt.Println("=== 2. Récupération et filtrage des Todos pour UserID = 1 ===")
	todos, err := getTodosByUser(1)
	if err != nil {
		log.Fatalf("Erreur : %v", err)
	}

	fmt.Println("Tâches complétées :")
	completedCount := 0
	for _, t := range todos {
		if t.Completed {
			completedCount++
			fmt.Printf("- [%d] %s\n", t.ID, t.Title)
		}
	}
	fmt.Printf("Total de tâches complétées : %d / %d\n\n", completedCount, len(todos))

	// Test du Challenge optionnel (Gestion du 404)
	fmt.Println("=== 3. Test du Challenge (Ressource inexistante) ===")
	_, errNotFound := getTodoByID(9999)
	if errNotFound != nil {
		fmt.Printf("Gestion d'erreur réussie : %v\n", errNotFound)
	}
}
```

---

## Explications pédagogiques et erreurs fréquentes

1. **Pointeurs dans `json.Unmarshal` :**
   - *Erreur classique :* Passer `todo` au lieu de `&todo` (`json.Unmarshal(body, todo)`).
   - *Explication :* `json.Unmarshal` a besoin de modifier la variable en mémoire, il est donc impératif de passer un pointeur.

2. **Fermeture des ressources (`defer resp.Body.Close()`) :**
   - Insister sur l'emplacement du `defer` : immédiatement **après** la vérification d'erreur (`if err != nil`). Si `resp` est `nil`, appeler `resp.Body.Close()` provoque un *panic*.

3. **Struct Tags (`json:"userId"`) :**
   - Expliquer l'écart entre les conventions Go (CamelCase avec initiale en majuscule pour l'exportation des champs, ex: `UserID`) et JSON (`userId`). Sans le tag, `Unmarshal` n'associera pas correctement la valeur sauf si la casse correspond.