---
## TP : API REST pour gestion d’une liste de tâches en Go

### Objectif  
Développer une API REST simple en Go permettant de créer, lire, mettre à jour et supprimer (CRUD) des tâches stockées en mémoire.

---

### Enoncé

Vous allez créer un serveur HTTP en Go exposant une API REST qui gère une liste de tâches. Chaque tâche a au minimum :

- Un identifiant unique (ID)
- Un titre (string)
- Un statut "complété" (booléen)

L’API doit offrir les endpoints suivants :

| Méthode | Endpoint     | Fonctionnalité                      |
|---------|--------------|-----------------------------------|
| GET     | /tasks       | Retourne la liste de toutes les tâches |
| GET     | /tasks/{id}  | Retourne une tâche par son ID      |
| POST    | /tasks       | Crée une nouvelle tâche            |
| PUT     | /tasks/{id}  | Modifie une tâche existante        |
| DELETE  | /tasks/{id}  | Supprime une tâche                 |

---

### Contraintes et détails

- Les données sont conservées uniquement en mémoire (pas de stockage permanent).
- Les IDs peuvent être auto-incrémentés ou générés dynamiquement.
- Utilisez uniquement la bibliothèque standard de Go (`net/http`, `encoding/json`…).
- Vos réponses doivent être au format JSON, avec les codes HTTP appropriés (200, 201, 404, 400…).
- Gérez les erreurs basiques : tâche non trouvée, mauvaise requête…
- Organisez le code en fonctions ou méthodes clairement nommées.
- Les requêtes POST et PUT doivent accepter des données JSON dans le corps.

---

### Quelques pistes

- Définissez une structure `Task` avec les champs nécessaires.
- Créez une slice ou map globale pour stocker les tâches.
- Écrivez des fonctions handler pour chaque endpoint, en utilisant `http.HandleFunc`.
- Pour extraire l’ID depuis l’URL, vous pouvez utiliser un simple parsing manuel de la chaîne.
- Convertissez les structures Go vers JSON avec `encoding/json`.
- Testez votre API avec curl, Postman ou directement via des requêtes en Go.

---

### Bonus (facultatif)

- Ajoutez un champ "description" facultatif aux tâches.
- Mettez en place un filtre simple sur `/tasks` pour ne retourner que les tâches complétées ou non (via paramètre query).
- Étendez la gestion des erreurs avec plus de détails dans les réponses JSON.

---

### Exemple minimal attendu  

```go
type Task struct {
    ID        int    `json:"id"`
    Title     string `json:"title"`
    Completed bool   `json:"completed"`
}
```

---

N’hésitez pas à vous appuyer sur GPT ou toute autre IA pour accélérer votre développement, mais tâchez de comprendre chaque partie du code que vous intégrez. Le but est de pratiquer Go et REST en contexte réel, en construisant étape par étape.

Bon code !