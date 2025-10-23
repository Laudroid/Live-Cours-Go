
#  Thème – Boucles imbriquées et affichage de motifs

---

### **Exercice 1 — Ligne d’étoiles**

####  **Objectif :**

Découvrir la boucle `for` et la répétition d’un caractère sur une seule ligne.

####  **Consigne :**

Affiche une ligne de **10 étoiles** :

```
**********
```

####  **Correction :**

```go
package main

import "fmt"

func main() {
    for i := 0; i < 10; i++ {
        fmt.Print("*") // Affiche une étoile sans retour à la ligne
    }
    fmt.Println() // Passe à la ligne après la boucle
}
```

####  **Explication pédagogique :**

* `for i := 0; i < 10; i++` → répète 10 fois.
* `fmt.Print()` n’ajoute pas de retour à la ligne, contrairement à `fmt.Println()`.
* Le `fmt.Println()` final permet de finir proprement la ligne.

---

### **Exercice 2 — Carré plein d’étoiles**

####  **Objectif :**

Utiliser des boucles imbriquées (`for` dans `for`).

####  **Consigne :**

Affiche un carré de 10x10 :

```
**********
**********
**********
**********
**********
**********
**********
**********
**********
**********
```

####  **Correction :**

```go
package main

import "fmt"

func main() {
    for i := 0; i < 10; i++ { // Gère les lignes
        for j := 0; j < 10; j++ { // Gère les colonnes
            fmt.Print("*")
        }
        fmt.Println() // Retour à la ligne après chaque rangée
    }
}
```

####  **Explication pédagogique :**

* La première boucle crée **10 lignes**.
* La deuxième crée **10 étoiles par ligne**.
* `Print` pour chaque étoile, `Println` après chaque ligne → un motif carré.

---

### **Exercice 3 — Carré vide**

####  **Objectif :**

Créer un motif creux à l’aide de conditions dans une double boucle.

####  **Consigne :**

Affiche un carré vide :

```
**********
*        *
*        *
*        *
*        *
*        *
*        *
*        *
*        *
**********
```

####  **Correction :**

```go
package main

import "fmt"

func main() {
    taille := 10

    for i := 0; i < taille; i++ { // Parcourt les lignes
        for j := 0; j < taille; j++ { // Parcourt les colonnes
            // Si on est sur une bordure (haut, bas, gauche, droite)
            if i == 0 || i == taille-1 || j == 0 || j == taille-1 {
                fmt.Print("*")
            } else {
                fmt.Print(" ")
            }
        }
        fmt.Println()
    }
}
```

####  **Explication pédagogique :**

* Bordures hautes/basses : `i == 0` ou `i == taille-1`.
* Bordures gauche/droite : `j == 0` ou `j == taille-1`.
* L’intérieur est rempli d’espaces `" "`.

---

### **Exercice 4 — Triangle plein**

####  **Objectif :**

Utiliser des boucles dépendantes pour créer un motif croissant.

####  **Consigne :**

Affiche un triangle d’étoiles :

```
*
**
***
****
*****
******
*******
********
```

####  **Correction :**

```go
package main

import "fmt"

func main() {
    lignes := 8

    for i := 1; i <= lignes; i++ {
        for j := 1; j <= i; j++ { // Le nombre d’étoiles augmente à chaque ligne
            fmt.Print("*")
        }
        fmt.Println()
    }
}
```

####  **Explication pédagogique :**

* Pour la ligne `i`, on affiche `i` étoiles.
* Le triangle croît naturellement : 1, 2, 3, 4… étoiles.
* On peut changer la variable `lignes` pour modifier la taille du triangle.

---

### **Exercice 5 — Triangle vide**

####  **Objectif :**

Combiner boucles et conditions pour afficher un triangle creux avec une base pleine.

####  **Consigne :**

Affiche un triangle vide :

```
*
**
* *
*  *
*   *
*    *
*******
```

####  **Correction :**

```go
package main

import "fmt"

func main() {
    lignes := 7

    for i := 1; i <= lignes; i++ {
        for j := 1; j <= i; j++ {
            // Bordure gauche, droite ou dernière ligne
            if j == 1 || j == i || i == lignes {
                fmt.Print("*")
            } else {
                fmt.Print(" ")
            }
        }
        fmt.Println()
    }
}
```

####  **Explication pédagogique :**

* `j == 1` → première étoile (bord gauche).
* `j == i` → dernière étoile de la ligne (bord droit).
* `i == lignes` → dernière ligne remplie entièrement d’étoiles.
* L’intérieur est composé d’espaces, ce qui forme un triangle creux.

