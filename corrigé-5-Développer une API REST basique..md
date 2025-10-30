# Solution 1 : API REST simple avec map, gestion manuelle des routes et parsing basique

### 📄 Fichier `main.go`

```go
package main

import (
	"encoding/json"
	"fmt"
	"log"
	"net/http"
	"strconv"
	"strings"
	"time"
)

// --- Structure de données ---
type Task struct {
	ID        int    `json:"id"`
	Title     string `json:"title"`
	Completed bool   `json:"completed"`
}

// --- Données en mémoire ---
var (
	tasks  = make(map[int]Task)
	nextID = 1
)

// --- Handlers ---

// GET /tasks : liste toutes les tâches
func handleGetTasks(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")

	taskList := make([]Task, 0, len(tasks))
	for _, t := range tasks {
		taskList = append(taskList, t)
	}

	json.NewEncoder(w).Encode(taskList)
}

// GET /tasks/{id} : récupère une tâche par ID
func handleGetTaskByID(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")

	id, err := extractID(r.URL.Path)
	if err != nil {
		http.Error(w, "ID invalide", http.StatusBadRequest)
		return
	}

	task, exists := tasks[id]
	if !exists {
		http.Error(w, "Tâche non trouvée", http.StatusNotFound)
		return
	}

	json.NewEncoder(w).Encode(task)
}

// POST /tasks : crée une nouvelle tâche
func handleCreateTask(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")

	var newTask Task
	if err := json.NewDecoder(r.Body).Decode(&newTask); err != nil {
		http.Error(w, "JSON invalide", http.StatusBadRequest)
		return
	}

	if strings.TrimSpace(newTask.Title) == "" {
		http.Error(w, "Titre requis", http.StatusBadRequest)
		return
	}

	newTask.ID = nextID
	nextID++
	tasks[newTask.ID] = newTask

	w.WriteHeader(http.StatusCreated)
	json.NewEncoder(w).Encode(newTask)
}

// PUT /tasks/{id} : met à jour une tâche
func handleUpdateTask(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")

	id, err := extractID(r.URL.Path)
	if err != nil {
		http.Error(w, "ID invalide", http.StatusBadRequest)
		return
	}

	var updated Task
	if err := json.NewDecoder(r.Body).Decode(&updated); err != nil {
		http.Error(w, "JSON invalide", http.StatusBadRequest)
		return
	}

	task, exists := tasks[id]
	if !exists {
		http.Error(w, "Tâche non trouvée", http.StatusNotFound)
		return
	}

	if updated.Title != "" {
		task.Title = updated.Title
	}
	task.Completed = updated.Completed

	tasks[id] = task
	json.NewEncoder(w).Encode(task)
}

// DELETE /tasks/{id} : supprime une tâche
func handleDeleteTask(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")

	id, err := extractID(r.URL.Path)
	if err != nil {
		http.Error(w, "ID invalide", http.StatusBadRequest)
		return
	}

	if _, exists := tasks[id]; !exists {
		http.Error(w, "Tâche non trouvée", http.StatusNotFound)
		return
	}

	delete(tasks, id)
	w.WriteHeader(http.StatusNoContent)
}

// --- Utilitaire ---
// Extrait l’ID depuis le paramètre de requête "task" (ex: "/tasks?id=3" → 3)
func extractID(r *http.Request) (int, error) {
	idStr := r.URL.Query().Get("id")
	if idStr == "" {
		return 0, fmt.Errorf("paramètre 'task' manquant")
	}
	return strconv.Atoi(idStr)
}


// --- Main ---
func main() {
	mux := http.NewServeMux()

	mux.HandleFunc("/tasks", func(w http.ResponseWriter, r *http.Request) {
		switch r.Method {
		case http.MethodGet:
			handleGetTasks(w, r)
		case http.MethodPost:
			handleCreateTask(w, r)
		default:
			http.Error(w, "Méthode non autorisée", http.StatusMethodNotAllowed)
		}
	})

	mux.HandleFunc("/tasks/", func(w http.ResponseWriter, r *http.Request) {
		switch r.Method {
		case http.MethodGet:
			handleGetTaskByID(w, r)
		case http.MethodPut:
			handleUpdateTask(w, r)
		case http.MethodDelete:
			handleDeleteTask(w, r)
		default:
			http.Error(w, "Méthode non autorisée", http.StatusMethodNotAllowed)
		}
	})

	server := &http.Server{
		Addr:         ":8080",
		Handler:      mux,
		ReadTimeout:  5 * time.Second,
		WriteTimeout: 10 * time.Second,
	}

	log.Println("✅ Serveur démarré sur http://localhost:8080")
	if err := server.ListenAndServe(); err != nil {
		log.Fatal(err)
	}
}
```

---

## **Explication**

| Étape  | Élément              | Description                                              |
| ------ | -------------------- | -------------------------------------------------------- |
| **1**  | `Task` struct        | Représente une tâche (id, titre, completed).             |
| **2**  | `map[int]Task`       | Sert de base de données en mémoire.                      |
| **3**  | `nextID`             | Génère un ID auto-incrémenté.                            |
| **4**  | `handleGetTasks`     | Renvoie la liste complète au format JSON.                |
| **5**  | `handleGetTaskByID`  | Récupère une tâche à partir de l’ID dans l’URL.          |
| **6**  | `handleCreateTask`   | Lit le JSON du corps et crée une nouvelle tâche.         |
| **7**  | `handleUpdateTask`   | Met à jour le titre ou le statut d’une tâche existante.  |
| **8**  | `handleDeleteTask`   | Supprime une tâche par ID.                               |
| **9**  | `extractID()`        | Parse l’ID dans le chemin `/tasks/{id}`.                 |
| **10** | `http.NewServeMux()` | Router qui distribue les requêtes selon la méthode HTTP. |

---

## **Tests rapides avec cURL**

```bash
# Créer une tâche
curl -X POST -H "Content-Type: application/json" -d '{"title":"Faire les courses"}' http://localhost:8080/tasks

# Lister les tâches
curl http://localhost:8080/tasks

# Lire une tâche
curl http://localhost:8080/tasks/1

# Modifier une tâche
curl -X PUT -H "Content-Type: application/json" -d '{"completed":true}' http://localhost:8080/tasks/1

# Supprimer une tâche
curl -X DELETE http://localhost:8080/tasks/1
```

# Solution 2 : API REST avec gestion d’une slice et filtre simple sur complétées

```go
package main

import (
	"encoding/json"
	"fmt"
	"net/http"
	"strconv"
	"strings"
	"sync"
)

type Task struct {
	ID          int    `json:"id"`
	Title       string `json:"title"`
	Completed   bool   `json:"completed"`
	Description string `json:"description,omitempty"` // Champ bonus optionnel
}

var (
	tasks     []Task
	currentID = 0
	mu        sync.Mutex
)

func main() {
	http.HandleFunc("/tasks", tasksHandler)
	http.HandleFunc("/tasks/", taskHandler)

	fmt.Println("Server running on http://localhost:8080")
	http.ListenAndServe(":8080", nil)
}

func tasksHandler(w http.ResponseWriter, r *http.Request) {
	switch r.Method {
	case "GET":
		getTasksWithFilter(w, r)
	case "POST":
		postTask(w, r)
	default:
		methodNotAllowed(w)
	}
}

func taskHandler(w http.ResponseWriter, r *http.Request) {
	id, err := extractID(r.URL.Path)
	if err != nil {
		http.Error(w, "ID invalide", http.StatusBadRequest)
		return
	}
	switch r.Method {
	case "GET":
		getTask(w, id)
	case "PUT":
		putTask(w, r, id)
	case "DELETE":
		deleteTask(w, id)
	default:
		methodNotAllowed(w)
	}
}

func extractID(path string) (int, error) {
	parts := strings.Split(path, "/")
	if len(parts) < 3 {
		return 0, fmt.Errorf("chemin incomplet")
	}
	return strconv.Atoi(parts[2])
}

// GET /tasks?completed=true|false filtre sur l'état complété si param présent
func getTasksWithFilter(w http.ResponseWriter, r *http.Request) {
	mu.Lock()
	defer mu.Unlock()

	query := r.URL.Query()
	filterCompleted := query.Get("completed")

	filtered := []Task{}
	for _, t := range tasks {
		if filterCompleted == "" {
			filtered = append(filtered, t)
		} else {
			wantCompleted := filterCompleted == "true"
			if t.Completed == wantCompleted {
				filtered = append(filtered, t)
			}
		}
	}

	writeJSON(w, filtered)
}

func postTask(w http.ResponseWriter, r *http.Request) {
	var t Task
	if err := json.NewDecoder(r.Body).Decode(&t); err != nil || strings.TrimSpace(t.Title) == "" {
		http.Error(w, "Titre obligatoire et JSON valide requis", http.StatusBadRequest)
		return
	}

	mu.Lock()
	currentID++
	t.ID = currentID
	tasks = append(tasks, t)
	mu.Unlock()

	w.WriteHeader(http.StatusCreated)
	writeJSON(w, t)
}

func getTask(w http.ResponseWriter, id int) {
	mu.Lock()
	defer mu.Unlock()
	for _, t := range tasks {
		if t.ID == id {
			writeJSON(w, t)
			return
		}
	}
	http.Error(w, "Tâche non trouvée", http.StatusNotFound)
}

func putTask(w http.ResponseWriter, r *http.Request, id int) {
	var upd Task
	if err := json.NewDecoder(r.Body).Decode(&upd); err != nil || strings.TrimSpace(upd.Title) == "" {
		http.Error(w, "Titre obligatoire et JSON valide requis", http.StatusBadRequest)
		return
	}

	mu.Lock()
	defer mu.Unlock()

	for i, t := range tasks {
		if t.ID == id {
			tasks[i].Title = upd.Title
			tasks[i].Completed = upd.Completed
			tasks[i].Description = upd.Description
			writeJSON(w, tasks[i])
			return
		}
	}
	http.Error(w, "Tâche non trouvée", http.StatusNotFound)
}

func deleteTask(w http.ResponseWriter, id int) {
	mu.Lock()
	defer mu.Unlock()

	for i, t := range tasks {
		if t.ID == id {
			tasks = append(tasks[:i], tasks[i+1:]...)
			w.WriteHeader(http.StatusNoContent)
			return
		}
	}
	http.Error(w, "Tâche non trouvée", http.StatusNotFound)
}

func writeJSON(w http.ResponseWriter, v interface{}) {
	w.Header().Set("Content-Type", "application/json")
	json.NewEncoder(w).Encode(v)
}

func methodNotAllowed(w http.ResponseWriter) {
	http.Error(w, "Méthode non autorisée", http.StatusMethodNotAllowed)
}
```

### Explications

- Cette version stocke les tâches dans une slice, manipulation plus simple à comprendre pour certains débutants.
- Ajout d’un champ optionnel `Description` au `Task` (bonus).
- Support d’un filtre simple via query parameter `completed` sur `/tasks` pour retourner uniquement tâches complétées ou non.
- Extraction de l’ID via découpage de l’URL, vérification et conversion en int.
- Utilisation d’un mutex pour protéger les accès concurrents.
- Fonctions organisées, avec gestion propre des erreurs et réponses JSON standardisées.
- Fonction utilitaire `writeJSON` pour réduire la duplication.

---

Ces deux exemples montrent des approches différentes pour construire une API REST en Go avec la bibliothèque standard :  
- Une avec `map` qui est efficace pour recherche rapide par ID,  
- Une autre avec slice plus adaptée à une liste ordonnée et au filtrage simple.  

Dans les deux cas, vous pratiquez la gestion des requêtes, du JSON, des routes basiques, et des erreurs HTTP.