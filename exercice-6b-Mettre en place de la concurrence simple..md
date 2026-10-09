---

# TP : Concours simple avec goroutines et channels

## Objectif  
Écrire un programme Go qui lance plusieurs goroutines exécutant indépendamment une tâche simple et qui collecte leurs résultats via un channel.

---

## Énoncé  

1. Crée une fonction `worker(id int, c chan<- string)` qui simule un travail en :  
   - affichant un message indiquant que la goroutine `id` démarre,  
   - dormant un court instant (par exemple, 1 à 3 secondes, choisi aléatoirement),  
   - envoyant un message de résultat (ex : `"Worker 3 terminé"`) sur le channel `c`.

2. Dans la fonction `main()`:  
   - crée un channel de chaîne de caractères adapté,  
   - lance 5 goroutines `worker` en leur passant chacune un identifiant unique (1 à 5),  
   - récupère et affiche les résultats de toutes les goroutines via le channel.

3. Assure-toi que le programme ne se termine qu’après réception des 5 résultats.

---

## Points clés à mettre en œuvre

- Utilisation des goroutines pour exécuter du code en concurrence.  
- Utilisation des channels pour la communication et la synchronisation.  
- Gestion du temps aléatoire pour simuler un travail variable.  
- Attention à la fermeture du channel : dans cet exercice, pas besoin de fermer le channel car on sait exactement combien de messages attendre.  

---

## Suggestions  

- Tu peux utiliser `time.Sleep()` et `time.Duration` pour simuler la pause.  
- La fonction `rand.Intn()` peut servir à générer la durée aléatoire (pense à initialiser la seed).  
- Tester ton code étape par étape facilite la compréhension.  

---

## Bonus (facultatif)  

- Modifier le programme pour que chaque goroutine retourne un entier (ex : le temps de pause), et calculer la somme de ces valeurs dans `main`.  
- Utiliser un `sync.WaitGroup` pour attendre la fin des goroutines au lieu de compter via le channel.  

---

Si tu utilises une IA pour t’aider, profite-en pour poser des questions précises sur ces concepts et vérifier ensemble la qualité du code produit. Bonne pratique !