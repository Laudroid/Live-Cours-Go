
# Thème 1 – Types et variables

---

### **Exercice 1 — Bonjour Go !**

####  **Énoncé :**

Écris un programme qui affiche « Bonjour, Go ! ».

####  **Correction :**

```go
package main

import "fmt"

func main() {
    fmt.Println("Bonjour, Go !")
}
```

####  **Explication :**

* `package main` : point d’entrée obligatoire d’un programme Go.
* `import "fmt"` : permet d’utiliser les fonctions d’affichage (`Println`).
* `func main()` : fonction principale, exécutée au démarrage.

---

### **Exercice 2 — Déclaration de variables**

####  **Énoncé :**

Déclare trois variables et affiche-les dans une phrase.

####  **Correction :**

```go
package main

import "fmt"

func main() {
    var nom string = "Alice"
    var age int = 20
    var taille float64 = 1.65

    fmt.Printf("Je m'appelle %s, j'ai %d ans et je mesure %.2f m.\n", nom, age, taille)
}
```

####  **Explication :**

* `%s`, `%d`, `%.2f` : formats de chaînes, entiers et flottants (2 décimales).
* `Printf` permet d’insérer des variables dans une phrase formatée.

---

### **Exercice 3 — Conversion de types**

####  **Énoncé :**

Demande un entier et affiche sa version float.

####  **Correction :**

```go
package main

import "fmt"

func main() {
    var entier int
    fmt.Print("Entrez un nombre entier : ")
    fmt.Scan(&entier)

    flottant := float64(entier)
    fmt.Println("Version float :", flottant)
}
```

####  **Explication :**

* `fmt.Scan(&entier)` lit la saisie utilisateur.
* Conversion explicite : `float64(entier)`.

---

### **Exercice 4 — Constantes et opérateurs**

####  **Énoncé :**

Calcule la surface d’un cercle.

####  **Correction :**

```go
package main

import "fmt"

func main() {
    const pi = 3.14159
    var rayon float64 = 5.0

    surface := pi * rayon * rayon
    fmt.Println("Surface du cercle :", surface)
}
```

####  **Explication :**

* `const` : valeur fixe non modifiable.
* L’opérateur `*` fait la multiplication.

---

### **Exercice 5 — Lecture clavier**

####  **Énoncé :**

Demande le prénom de l’utilisateur et salue-le.

####  **Correction :**

```go
package main

import "fmt"

func main() {
    var prenom string
    fmt.Print("Entrez votre prénom : ")
    fmt.Scan(&prenom)
    fmt.Println("Bonjour,", prenom, "!")
}
```

####  **Explication :**

* `Scan` récupère la saisie clavier.
* L’opérateur `,` concatène les éléments dans `Println`.

---

```go
Variante avec le prénom et le nom sur la même ligne :

func main() {
	var prenom, nom string

	fmt.Print("Entrez votre prénom et votre nom : ")
	fmt.Scan(&prenom, &nom)

	fmt.Printf("Bonjour %s %s !\n", prenom, nom)
}
```

#  Thème 2 – Boucles et conditions

---

### **Exercice 6 — Pair ou impair**

####  **Correction :**

```go
package main

import "fmt"

func main() {
    var n int
    fmt.Print("Entrez un nombre : ")
    fmt.Scan(&n)

    if n%2 == 0 {
        fmt.Println("Le nombre est pair.")
    } else {
        fmt.Println("Le nombre est impair.")
    }
}
```

####  **Explication :**

* `%` calcule le reste de la division.
* `if / else` contrôle le flux.

---

### **Exercice 7 — Maximum de deux nombres**

####  **Correction :**

```go
package main

import "fmt"

func main() {
    var a, b int
    fmt.Print("Entrez deux nombres : ")
    fmt.Scan(&a, &b)

    if a > b {
        fmt.Println("Le plus grand est :", a)
    } else {
        fmt.Println("Le plus grand est :", b)
    }
}
```

---

### **Exercice 8 — Compteur avec for**

####  **Correction :**

```go
package main

import "fmt"

func main() {
    for i := 1; i <= 10; i++ {
        fmt.Print(i, " ")
    }
    fmt.Println()
}
```

---

### **Exercice 9 — Somme des n premiers entiers**

####  **Correction :**

```go
package main

import "fmt"

func main() {
    var n, somme int
    fmt.Print("Entrez un nombre : ")
    fmt.Scan(&n)

    for i := 1; i <= n; i++ {
        somme += i
    }

    fmt.Println("La somme est :", somme)
}
```

---

### **Exercice 10 — Table de multiplication**

####  **Correction :**

```go
package main

import "fmt"

func main() {
    for i := 1; i <= 10; i++ {
        for j := 1; j <= 10; j++ {
            fmt.Printf("%4d", i*j)
        }
        fmt.Println()
    }
}
```

####  **Explication :**

* `fmt.Printf("%4d")` aligne les nombres dans une colonne de 4 caractères.

---

# Thème 3 – Tableaux, slices et maps

---

### **Exercice 11 — Tableau fixe**

####  **Correction :**

```go
package main

import "fmt"

func main() {
    nombres := [5]int{2, 4, 6, 8, 10}
    somme := 0

    for _, v := range nombres {
        somme += v
    }

    fmt.Println("Somme =", somme)
}
```

#### **Explication :**

* `range` parcourt chaque élément.
* `_` ignore l’indice.

---

### **Exercice 12 — Slice dynamique**

####  **Correction :**

```go
package main

import "fmt"

func main() {
    var n int
    fmt.Print("Combien de notes ? ")
    fmt.Scan(&n)

    notes := make([]float64, n)
    var somme float64

    for i := 0; i < n; i++ {
        fmt.Printf("Note %d : ", i+1)
        fmt.Scan(&notes[i])
        somme += notes[i]
    }

    moyenne := somme / float64(n)
    fmt.Println("Moyenne =", moyenne)
}
```

---

### **Exercice 13 — Append et copie**

####  **Correction :**

```go
package main

import "fmt"

func main() {
    nombres := []int{1, 2, 3}
    nombres = append(nombres, 4, 5, 6)

    fmt.Println("Slice :", nombres)
    fmt.Println("Longueur :", len(nombres))
}
```

---

### **Exercice 14 — Maps**

####  **Correction :**

```go
package main

import "fmt"

func main() {
    capitales := map[string]string{
        "France": "Paris",
        "Italie": "Rome",
        "Espagne": "Madrid",
    }

    var pays string
    fmt.Print("Entrez un pays : ")
    fmt.Scan(&pays)

    capitale, existe := capitales[pays]
    if existe {
        fmt.Println("La capitale est :", capitale)
    } else {
        fmt.Println("Pays inconnu.")
    }
}
```

---

### **Exercice 15 — Comptage des occurrences**

####  **Correction :**

```go
package main

import "fmt"

func main() {
    texte := "gogogo"
    compte := make(map[rune]int)

    for _, lettre := range texte {
        compte[lettre]++
    }

    fmt.Println("Occurrences :")
    for k, v := range compte {
        fmt.Printf("%c : %d\n", k, v)
    }
}
```

---

#  Thème 4 – Fonctions

---

### **Exercice 16 — Fonction simple**

####  **Correction :**

```go
package main

import "fmt"

func bonjour(nom string) {
    fmt.Println("Bonjour,", nom, "!")
}

func main() {
    bonjour("Alice")
}
```

---

### **Exercice 17 — Fonction avec retour**

####  **Correction :**

```go
package main

import "fmt"

func carre(x int) int {
    return x * x
}

func main() {
    fmt.Println("Le carré de 5 est :", carre(5))
}
```

---

### **Exercice 18 — Fonction avec plusieurs retours**

####  **Correction :**

```go
package main

import "fmt"

func divmod(a, b int) (int, int) {
    return a / b, a % b
}

func main() {
    q, r := divmod(17, 5)
    fmt.Println("Quotient :", q, "Reste :", r)
}
```

---

### **Exercice 19 — Fonction variadique**

####  **Correction :**

```go
package main

import "fmt"

func somme(nums ...int) int {
    total := 0
    for _, n := range nums {
        total += n
    }
    return total
}

func main() {
    fmt.Println("Somme =", somme(1, 2, 3, 4, 5))
}
```

####  **Explication :**

* `...int` permet de passer un nombre variable d’arguments.

---

### **Exercice 20 — Fonctions et slices**

####  **Correction :**

```go
package main

import "fmt"

func moyenne(notes []float64) float64 {
    var somme float64
    for _, n := range notes {
        somme += n
    }
    return somme / float64(len(notes))
}

func main() {
    notes := []float64{12.5, 15.0, 14.0, 16.5}
    fmt.Println("Moyenne :", moyenne(notes))
}
```

