# 1- Introduction au Go & bases du langage  
## 2- Bases du langage Go  
### 1- Déclaration de variables et types fondamentaux (int, float, string, bool)  

---

## 1. Déclaration des variables en Go  

### Syntaxes principales  

En Go, la déclaration des variables peut se faire de différentes manières en fonction du contexte :

- **Syntaxe classique avec `var` et typage explicite :**

```go
var a int = 10
var b string = "Hello"
var c bool = true
```

- **Déclaration avec inférence de type :**

Go peut déduire le type à partir de la valeur assignée :

```go
var a = 10       // a est de type int
var b = "World"  // b est de type string
```

- **Déclaration courte (usage fréquent dans les fonctions) :**

```go
a := 10
b := "GoLang"
```

Cette syntaxe fonctionne uniquement à l’intérieur des fonctions.

---

### Portée et utilisation

- Les variables déclarées avec `var` peuvent avoir une portée globale (en dehors d’une fonction) ou locale (à l’intérieur).
- La déclaration courte `:=` est strictement locale.

---

## 2. Types fondamentaux en Go  

Go est un langage strictement typé, avec des types de base bien définis.

### a) Type entier (`int`)

- Go propose plusieurs tailles d’entiers (`int8`, `int16`, `int32`, `int64`), mais la taille `int` dépend de la plateforme (32 ou 64 bits).
- Les entiers sont signés par défaut.  
- Pour les entiers non signés, on utilise `uint` et variantes (`uint8` équivaut à `byte`).

**Exemple :**

```go
var age int = 30
var score uint16 = 65535
```

---

### b) Type flottant (`float32`, `float64`)

- `float32` ou `float64` pour représenter les nombres à virgule flottante.
- La précision double (`float64`) est recommandée pour la plupart des calculs.

**Exemple :**

```go
var price float64 = 19.99
var rate float32 = 0.07
```

---

### c) Type chaîne de caractères (`string`)

- Les chaînes en Go sont immuables.
- Encodage UTF-8, ce qui permet d’utiliser des caractères Unicode facilement.
- Peut être entouré de guillemets doubles (`"`) pour des chaînes simples, ou de backquotes (`` ` ``) pour des chaînes brutes multi-lignes.

**Exemple :**

```go
var message string = "Bonjour, 世界"
rawString := `Chaîne
sur
plusieurs lignes`
```

---

### d) Type booléen (`bool`)

- Deux valeurs possibles : `true` ou `false`.
- Utilisé pour les conditions et flags.

**Exemple :**

```go
var isActive bool = true
var hasErrors bool
```

---

## 3. Exemple complet  

```go
package main

import "fmt"

func main() {
    var i int = 42
    j := 3.14
    var s string = "Go"
    b := false

    fmt.Println("Entier:", i)
    fmt.Println("Flottant:", j)
    fmt.Println("Chaîne :", s)
    fmt.Println("Booléen:", b)
}
```

---

## 4. Diagramme - cycle de vie d'une variable en Go

```mermaid
graph LR
    A[Déclaration] --> B[Initialisation]
    B --> C[Utilisation]
    C --> D[Modification (si possible)]
    D --> E[Fin de portée - libération]
```

- La variable est déclarée avec ou sans initialisation.
- Elle est utilisée/modifiée selon la logique.
- Lorsqu’elle sort de sa portée, Go gère automatiquement la libération mémoire grâce au ramasse-miettes (GC).

---

## Sources  

- Documentation officielle Go, "Variables": https://go.dev/doc/effective_go#variables  
- Tour of Go, "Variables and Types": https://tour.golang.org/basics/2  
- Golang Bot, "Go Data Types": https://golangbot.com/types/  
- Go by Example, "Variables": https://gobyexample.com/variables  
- Go Blog, "Introduction to Go": https://blog.golang.org/go-at-google  

---

Ce cours présente les fondamentaux de la déclaration de variables et des types primitifs en Go, permettant d’écrire du code clair, performant et typé strictement.