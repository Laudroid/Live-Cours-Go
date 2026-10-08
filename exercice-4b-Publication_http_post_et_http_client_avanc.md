# TP 2 : Envoi de Données HTTP POST et En-têtes Personnalisés en Go

**Prérequis :** Manipulation des structures Go, package `net/http` (notions de base).

---

## Objectifs pédagogiques
- Maîtriser la sérialisation (*marshalling*) de structures Go vers le format JSON.
- Envoyer des données au format JSON via une requête HTTP POST.
- Utiliser `http.Client` et `http.NewRequest` pour injecter des en-têtes HTTP personnalisés (`Content-Type`, `Authorization`).
- Analyser la réponse HTTP du serveur après création de ressource.

---

## Contexte et Matériel
L'entreprise dans laquelle vous travaillez souhaite intégrer un module Go permettant de publier de nouveaux articles d'actualité vers une plateforme distante via API REST. Vous devez créer une application en Go qui sérialise un objet, applique des critères de sécurité (jeton d'authentification) et transmet la donnée au serveur.

**URL d'API de test :**  
`https://jsonplaceholder.typicode.com/posts`

---

## Étape 1 : Modélisation et Marshalling

1. Dans un fichier `main.go`, définissez la structure `Article` :
   ```go
   type Article struct {
       ID     int    `json:"id,omitempty"`
       Title  string `json:"title"`
       Body   string `json:"body"`
       UserID int    `json:"userId"`
   }
   ```
2. Instanciez un objet `Article` avec des données fictives (`Title`, `Body`, `UserID`).
3. Convertissez cette structure en slice d'octets JSON (`[]byte`) à l'aide de `json.Marshal`.
4. Affichez la chaîne JSON obtenue sur la console afin de valider le format.

---

## Étape 2 : Envoi avec `http.Post`

1. Utilisez la fonction simplifiée `http.Post` pour envoyer votre chaîne JSON à l'URL `https://jsonplaceholder.typicode.com/posts`.
2. Assurez-vous de passer `application/json` comme type de contenu (*Header Content-Type*).
3. N'oubliez pas d'envelopper vos octets JSON dans un buffer avec `bytes.NewBuffer(jsonData)`.
4. Vérifiez que la réponse du serveur renvoie un code de création réussi (ex: `201 Created` / `http.StatusCreated`).
5. Affichez la réponse renvoyée par l'API.

---

## Étape 3 : Contrôle avancé avec `http.Client` et En-têtes

La fonction `http.Post` ne permet pas d'ajouter d'en-têtes spécifiques comme un token d'authentification Bearer. Vous allez refactoriser votre code :

1. Instanciez un client HTTP personnalisable :
   ```go
   client := &http.Client{}
   ```
2. Préparez la requête avec `http.NewRequest` :
   - Méthode : `"POST"`
   - URL : `"https://jsonplaceholder.typicode.com/posts"`
   - Corps : `bytes.NewBuffer(jsonData)`
3. Ajoutez les en-têtes suivants à la requête (`req.Header.Set`) :
   - `Content-Type`: `application/json`
   - `Authorization`: `Bearer my_secret_token_12345`
4. Exécutez la requête avec `client.Do(req)`.
5. Vérifiez les erreurs de transport et le code de statut HTTP.
6. Assurez-vous de libérer la mémoire avec `defer resp.Body.Close()`.

---

## Challenge optionnel / Aller plus loin

- Décodage de la réponse : L'API JSONPlaceholder renvoie l'objet créé avec son nouvel `id`.
- Récupérez le corps de la réponse de l'Étape 3 et décodez-le (`json.Unmarshal`) dans une nouvelle instance d'un `Article` pour afficher l'ID attribué par le serveur.
