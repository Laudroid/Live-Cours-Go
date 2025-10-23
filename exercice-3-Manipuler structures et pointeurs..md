# TP Go : Manipulation de structures et de pointeurs

## Objectif  
- Créer et manipuler une structure  
- Utiliser des pointeurs pour modifier des données passées en argument

---

## Enoncé

1. Définis une structure `Personne` qui contient :  
   - un champ `nom` de type `string`  
   - un champ `age` de type `int`  

2. Écris une fonction `modifierAge` qui :  
   - prend en paramètre un pointeur vers une `Personne`  
   - modifie l’âge de cette personne (en remplaçant l’âge actuel par celui passé en second paramètre)  

3. Dans `main` :  
   - crée une instance de `Personne`  
   - affiche ses valeurs initiales  
   - appelle `modifierAge` pour changer l’âge  
   - affiche les valeurs modifiées pour vérifier que la fonction agit bien sur la structure passée par pointeur  

---

## Contraintes / conseils  
- Ton code doit utiliser des pointeurs pour modifier l’objet passé, pas une copie  
- Affiche toujours les infos pour visualiser l’effet de ta fonction  
- N’hésite pas à commenter ton code pour clarifier la manipulation des pointeurs  
- Tu peux utiliser des outils d’IA pour t’aider, mais prends le temps de comprendre chaque ligne générée  
- Teste bien ce que tu écris, modifie les valeurs et vois si ça marche vraiment comme prévu  

---

## Exemple d’affichage attendu (à titre indicatif)

```bash
Avant modification : Nom=Alice, Age=30
Après modification : Nom=Alice, Age=35
```

---

## Bonus  
- Ajoute une fonction qui affiche les informations d’une `Personne` (en utilisant un pointeur)  
- Essaie de modifier le nom également via un pointeur (attention aux chaînes en Go)  

---

Bonne mise en pratique !