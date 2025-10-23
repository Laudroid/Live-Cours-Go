# Solution 1 : Fonction `SumInts` simple avec gestion d’erreur et test dans main

```go
package main

import (
    "errors"
    "fmt"
)

// SumInts calcule la somme des entiers dans le slice nums
// Retourne une erreur si le slice est vide.
func SumInts(nums []int) (int, error) {
    if len(nums) == 0 {
        return 0, errors.New("le tableau est vide")
    }
    sum := 0
    for _, v := range nums {
        sum += v
    }
    return sum, nil
}

func main() {
    numbers := []int{10, 15, 17}
    sum, err := SumInts(numbers)
    if err != nil {
        fmt.Println("Erreur:", err)
    } else {
        fmt.Println("Somme:", sum)
    }

    empty := []int{}
    sum, err = SumInts(empty)
    if err != nil {
        fmt.Println("Erreur:", err)
    } else {
        fmt.Println("Somme:", sum)
    }
}
```

### Explications

- La fonction contrôle d'abord si le slice est vide (`len(nums) == 0`).
- Si vide, elle retourne l’erreur construite avec `errors.New`.
- Sinon, elle parcourt le slice avec une boucle `for` classique et additionne les éléments.
- Le `main` teste les deux cas : slice non vide et vide, et affiche clairement la sortie.
- Code clair, concis, idéale pour comprendre le contrôle d’erreur en Go.

---

# Solution 2 : Ajout d’une fonction `AverageInts` réutilisant `SumInts` avec gestion d’erreur

```go
package main

import (
    "errors"
    "fmt"
)

// SumInts retourne la somme des éléments d'un slice ou une erreur si vide.
func SumInts(nums []int) (int, error) {
    if len(nums) == 0 {
        return 0, errors.New("le tableau est vide")
    }
    sum := 0
    for _, v := range nums {
        sum += v
    }
    return sum, nil
}

// AverageInts calcule la moyenne des entiers dans nums en réutilisant SumInts
// Retourne une erreur si slice vide (pour éviter division par zéro).
func AverageInts(nums []int) (float64, error) {
    sum, err := SumInts(nums)
    if err != nil {
        return 0, err // Propagation de l'erreur
    }
    avg := float64(sum) / float64(len(nums))
    return avg, nil
}

func main() {
    numbers := []int{10, 15, 17}

    sum, err := SumInts(numbers)
    if err != nil {
        fmt.Println("Erreur:", err)
    } else {
        fmt.Println("Somme:", sum)
    }

    avg, err := AverageInts(numbers)
    if err != nil {
        fmt.Println("Erreur moyenne:", err)
    } else {
        fmt.Printf("Moyenne: %.2f\n", avg)
    }

    empty := []int{}

    // Test somme vide
    sum, err = SumInts(empty)
    if err != nil {
        fmt.Println("Erreur:", err)
    } else {
        fmt.Println("Somme:", sum)
    }

    // Test moyenne vide
    avg, err = AverageInts(empty)
    if err != nil {
        fmt.Println("Erreur moyenne:", err)
    } else {
        fmt.Printf("Moyenne: %.2f\n", avg)
    }
}
```

### Explications

- `AverageInts` fait appel à `SumInts` pour récupérer la somme et gérer l’erreur de tableau vide.
- Elle convertit ensuite la somme en `float64` pour la division, évitant ainsi une division entière.
- Gère explicitement le cas du tableau vide pour éviter la division par zéro en renvoyant la même erreur.
- Offre un exemple clair de réutilisation fonctionnelle et gestion d’erreurs en cascade.
- L'affichage dans `main` montre clairement les résultats et les erreurs pour les deux fonctions.

---

Ces solutions couvrent les points demandés : déclaration, gestion d’erreurs, test et réutilisation fonctionnelle.  
N’hésite pas à expérimenter avec différentes tailles de tableaux ou à intégrer des tests unitaires Go pour aller plus loin.