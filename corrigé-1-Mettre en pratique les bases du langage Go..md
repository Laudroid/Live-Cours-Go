# Solution 1 : Utilisation de fmt.Scanln()

```go
package main

import (
    "fmt"
)

func main() {
    // Afficher Bonjour, Go!
    fmt.Println("Bonjour, Go!")

    // Demander le nom
    fmt.Print("Entrez votre nom : ")

    // Variable pour stocker la saisie
    var name string

    // Lire la saisie; Scanln attend une entrée terminée par un retour à la ligne,
    // elle lit jusqu’au premier espace ou fin de ligne
    fmt.Scanln(&name)

    // Afficher le message personnalisé
    // Si l'utilisateur n'a rien saisi, name sera vide
    if name == "" {
        fmt.Println("Vous n'avez rien saisi.")
    } else {
        fmt.Printf("Bonjour, %s !\n", name)
    }
}
```

### Explications

- `fmt.Scanln(&name)` lit la première "mot" entrée (jusqu’au premier espace ou retour à la ligne). Si l’utilisateur tape plusieurs mots, seul le premier est pris en compte.
- Si l'entrée est vide (l'utilisateur appuie juste sur Entrée), la variable `name` reste vide, ce qui permet d’ajouter une condition simple pour gérer ce cas.
- Cette solution est simple et idiomatique pour des saisies courtes sans espaces.

---

# Solution 2 : Utilisation de bufio.NewReader(os.Stdin) pour gérer des noms avec espaces

```go
package main

import (
    "bufio"
    "fmt"
    "os"
    "strings"
)

func main() {
    fmt.Println("Bonjour, Go !")

    reader := bufio.NewReader(os.Stdin) // Crée un lecteur du flux standard

    fmt.Print("Entrez votre nom : ")
    input, err := reader.ReadString('\n') // Lit jusqu'au saut de ligne
    if err != nil {
        fmt.Println("Erreur de lecture :", err)
        return
    }

    // Nettoyer l'entrée : supprimer espaces en début/fin et le saut de ligne '\n'
    input = strings.TrimSpace(input)

    if input == "" {
        fmt.Println("Vous n'avez rien saisi.")
    } else {
        fmt.Printf("Bonjour, %s !\n", input)
    }
}
```

### Explications

- `bufio.NewReader(os.Stdin)` permet de lire une ligne entière, incluant des espaces, jusqu’au retour à la ligne.
- `ReadString('\n')` lit tout ce que l'utilisateur tape jusque l'appui sur Entrée.
- `strings.TrimSpace` retire les espaces en début et fin de chaîne, ainsi que le caractère de nouvelle ligne.
- Ce qui permet d'accepter des noms composés avec espaces et d’éviter les erreurs dues à des espaces parasites.

---

Ces deux solutions sont complètes pour répondre au TP. La première est plus rapide pour un nom simple, la seconde plus robuste pour des entrées plus complexes.  
N'hésitez pas à me demander une version avec boucle pour plusieurs saisies si vous le souhaitez.