---
# TP Langage Go : Consommer une API web via une requête GET

## Objectif  
Écrire un programme Go qui effectue une requête HTTP GET vers une API publique, récupère une réponse JSON, la parse pour extraire des informations, puis affiche ces données dans la console.

---

## Enoncé

1. Choisissez une API publique simple et sans authentification, par exemple :  
   - https://jsonplaceholder.typicode.com/posts/1  
   - https://api.coindesk.com/v1/bpi/currentprice.json  
   - https://dog.ceo/api/breeds/image/random

2. Écrire un programme qui :  
   - Envoie une requête GET à cette API (utiliser `net/http`)  
   - Lit la réponse et la convertit en chaîne JSON  
   - Parse ce JSON en structures Go (`struct`) adaptées (utiliser `encoding/json`)  
   - Affiche dans la console une ou plusieurs informations pertinentes provenant de l’API (par exemple, le titre d’un post, le taux du bitcoin, ou l’URL d’une image de chien)  

---

## Contraintes / conseils

- Créez des types Go correspondant strictement à la structure JSON que vous allez recevoir, pas trop généraux, pour pratiquer le mapping structuré.  
- Gérez les erreurs jusqu’à l’affichage (requête, lecture, parsing).  
- Utilisez les bonnes pratiques de Go (gestion des erreurs, nommage, idiomes).  
- Vous pouvez vous faire aider par l’IA pour générer les structs ou le squelette du code, mais vérifiez et comprenez bien les résultats.  
- Commenter uniquement les parties techniques que vous pensez utiles, évitez les commentaires redondants.  

---

## Exemple d’API choisie

Avec l’API `https://jsonplaceholder.typicode.com/posts/1`, on reçoit un JSON ressemblant à :

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae..."
}
```

À afficher dans la console :  
`Post #1: sunt aut facere repellat provident occaecati excepturi optio reprehenderit`

---

## Bonus (optionnel)

- Traitez un tableau JSON (exemple : `/posts`) et affichez les titres des 5 premiers posts.  
- Ajoutez un délai entre plusieurs requêtes (gestion simple de concurence avec `time.Sleep`).  
- Implémentez un retry simple en cas d’erreur réseau.  

---

## Livraison

- Documentez le choix de l’API et les données affichées.  
- Livrez un seul fichier `.go` compilable et commenté avec vos observations sur le parsing JSON.  

---

Ce travail s’inscrit dans la compréhension concrète des échanges entre un client Go et une API web, ainsi que dans la maîtrise du parsing JSON. Bonne exploration !