# Solution 1 : Consommer l’API JSONPlaceholder pour un post unique

```go
package main

import (
	"encoding/json"
	"fmt"
	"io/ioutil"
	"net/http"
)

// Post correspond à la structure JSON retournée par l'API
type Post struct {
	UserID int    `json:"userId"`
	ID     int    `json:"id"`
	Title  string `json:"title"`
	Body   string `json:"body"`
}

func main() {
	url := "https://jsonplaceholder.typicode.com/posts/1"

	resp, err := http.Get(url)
	if err != nil {
		fmt.Println("Erreur lors de la requête HTTP :", err)
		return
	}
	defer resp.Body.Close()

	body, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		fmt.Println("Erreur lors de la lecture de la réponse :", err)
		return
	}

	var post Post
	err = json.Unmarshal(body, &post)
	if err != nil {
		fmt.Println("Erreur lors du parsing JSON :", err)
		return
	}

	// Affichage d'une information pertinente issue de l'API
	fmt.Printf("Post #%d: %s\n", post.ID, post.Title)
}
```

### Explications

- L’URL cible renvoie un objet JSON représentant un post.
- La struct `Post` a été définie avec des tags `json` pour un mapping précis.
- Après la requête `http.Get`, on récupère le body puis on décode le JSON en struct.
- En cas d’erreur à chaque étape, on affiche un message explicite.
- L’affichage final ne présente que le titre du post, clair et concis.

---

# Solution 2 : Consommer l’API Dog CEO pour une image aléatoire de chien + retry simple

```go
package main

import (
	"encoding/json"
	"errors"
	"fmt"
	"net/http"
	"time"
)

// ApiResponse représente la structure JSON retournée par l'API Dog CEO
type ApiResponse struct {
	Message string `json:"message"` // URL de l'image
	Status  string `json:"status"`  // success ou autre
}

// getWithRetry effectue une requête GET avec retry simple en cas d'erreur réseau
func getWithRetry(url string, retries int, delay time.Duration) (*http.Response, error) {
	for i := 0; i <= retries; i++ {
		resp, err := http.Get(url)
		if err == nil && resp.StatusCode == http.StatusOK {
			return resp, nil
		}
		if resp != nil {
			resp.Body.Close()
		}
		if i < retries {
			time.Sleep(delay)
		}
	}
	return nil, errors.New("échec de la requête après plusieurs tentatives")
}

func main() {
	url := "https://dog.ceo/api/breeds/image/random"

	resp, err := getWithRetry(url, 3, 2*time.Second)
	if err != nil {
		fmt.Println("Erreur lors de la requête avec retry :", err)
		return
	}
	defer resp.Body.Close()

	var apiResp ApiResponse
	err = json.NewDecoder(resp.Body).Decode(&apiResp)
	if err != nil {
		fmt.Println("Erreur lors du décodage JSON :", err)
		return
	}

	if apiResp.Status != "success" {
		fmt.Println("Réponse API non réussie:", apiResp.Status)
		return
	}

	fmt.Println("URL d'une image aléatoire de chien :", apiResp.Message)
}
```

### Explications

- L’API Dog CEO retourne un JSON avec l’URL d’une image de chien.
- Le struct `ApiResponse` correspond strictement au JSON reçu avec des tags JSON.
- `getWithRetry` encapsule une logique simple de retry en cas d’erreur réseau ou statut HTTP non OK.
- Dans `main`, on récupère la réponse, on décode directement depuis `resp.Body` avec un `json.Decoder`.
- On valide que `status` vaut bien "success" avant d’afficher l’URL.
- Retard de 2 secondes entre tentatives, tentatives limitées à 3.

---

Ces deux exemples montrent la gestion classique de requêtes HTTP, parsing JSON structuré, gestion des erreurs et affichage ciblé.  
Adaptez les structs et la logique selon l’API choisie pour bien maîtriser les interactions web en Go.