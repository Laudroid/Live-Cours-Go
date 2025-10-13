# 2- Collections, fonctions et erreurs  
## 3- Gestion des erreurs  
### 3- Erreur personnalisée  

---

## 1. Pourquoi créer une erreur personnalisée ?  

Les erreurs simples créées avec `errors.New` ou `fmt.Errorf` contiennent un message texte mais ne permettent pas de transmettre des informations structurées ou de distinguer facilement différents types d’erreurs dans le code.  

Une erreur personnalisée, qui implémente l’interface `error`, permet :  
- de porter des données additionnelles  
- de catégoriser les erreurs par type  
- d’écrire un traitement spécifique selon le type d’erreur  

---

## 2. Définition d’une erreur personnalisée  

Il suffit de créer un type struct qui implémente la méthode `Error() string`.  

Exemple :

```go
type ErreurValidation struct {
    Champ   string
    Message string
}

func (e *ErreurValidation) Error() string {
    return fmt.Sprintf("Erreur dans le champ '%s' : %s", e.Champ, e.Message)
}
```

---

## 3. Utilisation d’une erreur personnalisée  

```go
package main

import (
    "fmt"
)

type ErreurValidation struct {
    Champ   string
    Message string
}

func (e *ErreurValidation) Error() string {
    return fmt.Sprintf("Erreur dans le champ '%s' : %s", e.Champ, e.Message)
}

func validerNom(nom string) error {
    if nom == "" {
        return &ErreurValidation{
            Champ:   "Nom",
            Message: "ne peut pas être vide",
        }
    }
    return nil
}

func main() {
    err := validerNom("")
    if err != nil {
        fmt.Println("Validation échouée :", err)
    } else {
        fmt.Println("Validation réussie")
    }
}
```

---

## 4. Types d’erreurs et assertion de type  

L’intérêt principal est de pouvoir détecter des erreurs spécifiques en utilisant une **assertion de type**. Cela permet un traitement dédié selon l’erreur.

```go
if err, ok := err.(*ErreurValidation); ok {
    fmt.Printf("Champ en erreur : %s\n", err.Champ)
} else {
    fmt.Println("Autre erreur :", err)
}
```

---

## 5. Exemple complet avec erreur personnalisée et gestion multiple  

```go
package main

import (
    "fmt"
)

type ErreurValidation struct {
    Champ   string
    Message string
}

func (e *ErreurValidation) Error() string {
    return fmt.Sprintf("erreur dans le champ '%s' : %s", e.Champ, e.Message)
}

func validerAge(age int) error {
    if age < 0 || age > 150 {
        return &ErreurValidation{
            Champ:   "Age",
            Message: "doit être compris entre 0 et 150",
        }
    }
    return nil
}

func main() {
    erreurs := []error{
        validerAge(-3),
        validerAge(34),
        validerAge(200),
    }

    for _, err := range erreurs {
        if err != nil {
            if e, ok := err.(*ErreurValidation); ok {
                fmt.Printf("Validation échouée sur %s : %s\n", e.Champ, e.Message)
            } else {
                fmt.Println("Erreur inconnue :", err)
            }
        } else {
            fmt.Println("Validation OK")
        }
    }
}
```

---

## 6. Diagramme Mermaid — interaction types error et gestion  

```mermaid
flowchart TD
    A[Fonction retourne une erreur] --> B{Erreur simple ?}
    B -- Oui --> C[Message texte]
    B -- Non --> D[Erreur personnalisée (struct)]
    D --> E[Possède champs additionnels]
    E --> F[Assertion de type possible]
    F --> G[Traitement adapté]
```

---

## 7. Points clés  

| Élément               | Détail                                               |
|-----------------------|-----------------------------------------------------|
| Interface `error`     | Must have `Error() string`                           |
| Erreur personnalisée  | Struct avec champs et méthode `Error()`             |
| Assertion de type     | Detecte type concret d'erreur                        |
| Utilisation pratique  | Transmission d’infos métier, décisions de contrôle  |

---

## Sources  

- Documentation officielle Go, "Errors": https://go.dev/doc/tutorial/error-handling  
- Go by Example, "Custom Errors": https://gobyexample.com/custom-error  
- Tour of Go, "Errors": https://go.dev/tour/moretypes/19  
- Effective Go, "Errors": https://golang.org/doc/effective_go#errors  

---

Cette approche rend la gestion d’erreurs plus fine et robuste, favorisant un code clair et évolutif, avec des erreurs compréhensibles enrichies d’informations supplémentaires.