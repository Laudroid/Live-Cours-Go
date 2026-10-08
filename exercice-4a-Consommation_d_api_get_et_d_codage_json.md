# TP 1 : Consommation d'une API REST GET et Décodage JSON en Go

**Prérequis :** Bases du langage Go, syntaxe des structures et pointeurs.

---

## Objectifs pédagogiques
- Comprendre le fonctionnement des requêtes HTTP GET avec le package `net/http`.
- Définir des structures Go adaptées aux réponses JSON avec les *struct tags*.
- Effectuer la désérialisation (*unmarshalling*) de données JSON.
- Gérer la fermeture des ressources (`resp.Body`) et les erreurs courantes.

---

## Contexte et Matériel
Vous devez développer un outil en ligne de commande (CLI) capable de communiquer avec l'API publique **JSONPlaceholder** pour afficher la liste des tâches (*todos*) associées à un utilisateur donné.

**URL de l'API :**  
`https://jsonplaceholder.typicode.com/todos`

---

## Étape 1 : Analyser la structure des données

1. Ouvrez votre navigateur ou utilisez un outil comme `curl` pour observer la réponse renvoyée par `https://jsonplaceholder.typicode.com/todos/1`.
2. Observez le format JSON suivant :
   ```json
   {
     "userId": 1,
     "id": 1,
     "title": "delectus aut autem",
     "completed": false
   }
   ```
3. Créez un fichier `main.go`. Définissez-y la structure Go `Todo` correspondant exactement au schéma ci-dessus. N'oubliez pas d'inclure les tags `json:"..."`.

---

## Étape 2 : Implémenter la requête GET

1. Écrivez une fonction `getTodoByID(id int) (*Todo, error)` qui :
   - Effectue une requête HTTP GET vers `https://jsonplaceholder.typicode.com/todos/<id>`.
   - Vérifie que le code de statut HTTP est égal à `http.StatusOK` (200).
   - Utilise `defer` pour fermer le corps de la réponse (`resp.Body`).
   - Lit le corps de la réponse avec `io.ReadAll`.
   - Utilise `json.Unmarshal` pour transformer le JSON dans une instance de votre structure `Todo`.
2. Dans la fonction `main()`, appelez `getTodoByID(1)` et affichez le résultat de manière lisible dans la console.

---

## Étape 3 : Traiter une liste d'éléments

1. Créez une seconde fonction `getTodosByUser(userID int) ([]Todo, error)` qui interroge l'URL :  
   `https://jsonplaceholder.typicode.com/todos?userId=<userID>`
2. La réponse du serveur est un **tableau JSON** (`[ { ... }, { ... } ]`). Adaptez la désérialisation pour obtenir un slice de `Todo` (`[]Todo`).
3. Dans la fonction `main()`, demandez ou définissez un `userID` (ex: `userID = 1`), puis filtrez en Go pour n'afficher que les tâches qui sont **terminées** (`completed: true`).

---

## Challenge optionnel / Aller plus loin

- Modifiez le programme pour gérer le cas où l'utilisateur demande une tâche inexistante (ex: `id = 9999`).
- Retournez une erreur explicite si le code de statut est `http.StatusNotFound` (404).

