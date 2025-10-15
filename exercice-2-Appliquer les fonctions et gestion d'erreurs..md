---
# TP Langage Go : Fonction de somme avec gestion d’erreurs

### Objectif  
Mettre en pratique la déclaration de fonctions, la gestion des valeurs de retour et la gestion d’erreur.

### Énoncé  
Écrire une fonction `SumInts` qui prend en paramètre un tableau (slice) d’entiers (`[]int`) et retourne :

- la somme des éléments du tableau,
- une erreur si le tableau est vide, sinon `nil`.

### Contraintes & indications  
- La fonction doit avoir la signature :  
  ```go
  func SumInts(nums []int) (int, error)
  ```
- Pour retourner une erreur, tu peux utiliser `errors.New` (package `errors`).
- Dans la fonction `main`, teste `SumInts` avec au moins ces cas : un tableau non vide et un tableau vide.
- Affiche clairement le résultat ou l’erreur retournée.
- Structure ton code pour que la fonction soit testable indépendamment du `main`.
- Exploite l’IA pour formuler tes questions, vérifier ta syntaxe ou améliorer ton code, en restant critique sur les réponses fournies.

### Exemple attendu de sortie  
```
Somme: 42
Erreur: le tableau est vide
```

### Bonus (facultatif)  
- Ajoute une fonction qui calcule la moyenne des entiers en réutilisant `SumInts`.
- Gère la division par zéro dans la fonction moyenne.

---

### Exemple minimal de squelette 

```go
package main

import (
	"errors"
	"fmt"
)

func SumInts(nums []int) (int, error) {
	// TODO
}

func main() {
	numbers := []int{10, 15, 17}
	sum, err := SumInts(numbers)
	// TODO
}
```
