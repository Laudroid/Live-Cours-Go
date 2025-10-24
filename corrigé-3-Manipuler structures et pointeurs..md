# Solution 1 : Modification de l’âge via pointeur simple + affichage direct dans main

```go
package main

import (
    "fmt"
)

// Définition de la structure Personne avec nom et âge
type Personne struct {
    nom string
    age int
}

// modifierAge modifie l'âge de la personne pointée par p
func modifierAge(p *Personne, nouvelAge int) {
    // On accède au champ age du pointeur et on le modifie directement
    p.age = nouvelAge
}

func main() {
    // Création et initialisation d'une instance Personne
    personne := Personne{nom: "Alice", age: 30}

    // Affichage avant modification
    fmt.Printf("Avant modification : Nom=%s, Age=%d\n", personne.nom, personne.age)

    // Modification de l'âge via un pointeur vers personne
    modifierAge(&personne, 35)

    // Affichage après modification
    fmt.Printf("Après modification : Nom=%s, Age=%d\n", personne.nom, personne.age)
}
```

### Explications

- La fonction `modifierAge` reçoit un pointeur `*Personne` (adresse mémoire), ce qui permet la modification directe de l’objet d’origine.
- En Go, l’accès à un champ via un pointeur est possible avec `p.age`, qui est équivalente à `(*p).age`.
- Toute modification de `p.age` agit sur la structure originale passée.
- L’affichage dans `main` avant et après démontre clairement l'effet.

---

# Solution 2 : Ajout d’une fonction d’affichage et modification du nom via pointeur

```go
package main

import (
    "fmt"
)

// Structure Personne avec nom et age
type Personne struct {
    nom string
    age int
}

// modifierAge modifie l'âge de la personne via pointeur
func modifierAge(p *Personne, nouvelAge int) {
    p.age = nouvelAge
}

// modifierNom change le nom de la personne via pointeur
func modifierNom(p *Personne, nouveauNom string) {
    p.nom = nouveauNom
}

// afficherPersonne affiche nom et âge en recevant un pointeur
func afficherPersonne(p *Personne) {
    fmt.Printf("Nom=%s, Age=%d\n", p.nom, p.age)
}

func main() {
    p := Personne{nom: "Alice", age: 30}

    fmt.Print("Avant modification : ")
    afficherPersonne(&p)

    modifierAge(&p, 35)       // Modification âge
    modifierNom(&p, "Bob")    // Modification nom

    fmt.Print("Après modification : ")
    afficherPersonne(&p)
}
```

### Explications

- La fonction `afficherPersonne` prend un pointeur pour éviter une copie inutile, bien que la copie d’une petite structure soit peu coûteuse ici.
- `modifierNom` montre un autre cas de modification via pointeur, cette fois sur une chaîne de caractères, qui en Go est un type immuable mais la réaffectation d’un champ `string` marche directement.
- Cette organisation améliore la lisibilité et modularité du code.
- Le passage de pointeur permet de travailler efficacement sur les objets originaux sans duplication.

---

Ces deux approches illustrent bien l’usage des pointeurs pour modifier des structures en Go, avec ou sans fonctions d'affichage dédiées.  
Tester ces codes permet de bien comprendre la manipulation mémoire indirecte par pointeur et l’effet sur les structures.