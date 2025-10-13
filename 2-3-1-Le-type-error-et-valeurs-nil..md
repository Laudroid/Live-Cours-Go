# 2- Collections, fonctions et erreurs  
## 3- Gestion des erreurs  
### 1- Le type error et valeurs nil  

---

## 1. Le type `error` en Go  

En Go, la gestion des erreurs est basée sur un type d'interface nommé `error`.

### Définition de l'interface `error`  

```go
type error interface {
    Error() string
}
```

Une **erreur** est donc toute valeur qui implémente cette interface, c’est-à-dire qui possède une méthode `Error()` retournant une chaîne descriptive.

---

## 2. Création d’erreurs  

### a) Utilisation de la fonction `errors.New`  

```go
import "errors"

err := errors.New("une erreur est survenue")
fmt.Println(err.Error())  // affiche : une erreur est survenue
```

`errors.New` crée une erreur simple avec le message spécifié.

### b) Erreurs formatées avec `fmt.Errorf`  

```go
import "fmt"

err := fmt.Errorf("erreur %d: %s", 404, "ressource non trouvée")
```

Cette fonction permet d’ajouter de la valeur dynamique dans le message.

---

## 3. Valeur `nil` pour l’erreur  

En Go, l'absence d'erreur est indiquée par la valeur spéciale `nil` (zéro valeur des pointeurs et interfaces).

```go
var err error = nil
if err == nil {
    fmt.Println("Pas d'erreur")
} else {
    fmt.Println("Erreur détectée :", err)
}
```

Lorsqu'une fonction retourne une erreur, elle retourne souvent `nil` si tout s’est bien passé, ce qui est la convention à suivre pour indiquer un succès.

---

## 4. Exemple d’usage courant avec retour d’erreur  

```go
package main

import (
    "errors"
    "fmt"
)

func division(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division par zéro interdite")
    }
    return a / b, nil
}

func main() {
    res, err := division(10, 0)
    if err != nil {
        fmt.Println("Erreur :", err)
    } else {
        fmt.Println("Résultat :", res)
    }
}
```

---

## 5. Comparaison d’erreur avec `nil`  

On teste systématiquement si une erreur est présente par comparaison à `nil`.

```go
if err != nil {
    // gérer l’erreur
}
```

---

## 6. Diagramme Mermaid - cycle de vie d'une erreur en Go  

```mermaid
flowchart TD
    A[Fonction appelée] --> B[Retourne (résultat, error)]
    B --> C{error == nil ?}
    C -- Oui --> D[Traitement normal]
    C -- Non --> E[Gestion de l'erreur]
```

---

## 7. Points clés  

| Concept         | Description                                  |
|-----------------|----------------------------------------------|
| Type `error`    | Interface avec méthode `Error() string`      |
| Création        | `errors.New` ou `fmt.Errorf`                  |
| Valeur `nil`    | Indique l’absence d’erreur                    |
| Vérification    | Toujours tester `if err != nil`               |
| Retour multiple | Souvent `(valeur, error)`                      |

---

## Sources  

- Documentation officielle Go, "Errors": https://go.dev/doc/tutorial/error-handling  
- Documentation officielle Go, package errors: https://pkg.go.dev/errors  
- Tour of Go, "Errors": https://go.dev/tour/moretypes/19  
- Go by Example, "Errors": https://gobyexample.com/errors  

---

Ce cours présente comment Go modélise les erreurs via l'interface `error` et l’importance d’une gestion explicite avec la valeur `nil`, garantissant un code clair et robuste.