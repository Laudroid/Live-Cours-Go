# 2- Collections, fonctions et erreurs  
## 1- Collections en Go  
### 2- Maps : déclaration, accès et modification  

---

## 1. Présentation des maps en Go  

Une **map** est une structure de données associative qui stocke des paires clé-valeur. Elle permet un accès rapide aux valeurs à partir de leurs clés.

### Syntaxe générale :

```go
map[TypeClé]TypeValeur
```

Par exemple, une map de chaînes indexées par des entiers : `map[int]string`.

---

## 2. Déclaration et initialisation  

### a) Déclaration d'une map vide  

```go
var m map[string]int  // nil, non initialisée
```

Cette déclaration crée une map nulle qui ne peut pas encore être utilisée ; il faut l'initialiser.

### b) Initialisation avec `make`  

```go
m = make(map[string]int)
```

### c) Déclaration et initialisation combinées  

```go
m := make(map[string]int)
```

ou avec des valeurs initiales :

```go
m := map[string]int{
    "a": 1,
    "b": 2,
}
```

---

## 3. Accès aux éléments  

- Lire une valeur par sa clé :

```go
val := m["a"]
```

- Pour savoir si une clé existe, on utilise l'assignation avec test booléen :

```go
val, ok := m["clé"]
if ok {
    fmt.Println("Valeur :", val)
} else {
    fmt.Println("Clé non trouvée")
}
```

---

## 4. Ajout, modification et suppression  

- **Ajouter ou modifier** une paire clé-valeur :  

```go
m["nouvelleclé"] = 10
```

- **Supprimer** une clé :

```go
delete(m, "cléASupprimer")
```

---

## 5. Parcours d'une map  

```go
for clé, val := range m {
    fmt.Println(clé, ":", val)
}
```

L’ordre dans lequel les paires sont retournées est non déterministe.

---

## 6. Exemple complet  

```go
package main

import "fmt"

func main() {
    // Déclaration et initialisation
    m := map[string]int{
        "pomme":  5,
        "banane": 7,
    }

    // Accès et test d'existence
    nbPommes, ok := m["pomme"]
    if ok {
        fmt.Println("Nombre de pommes :", nbPommes)
    }

    // Ajout / modification
    m["orange"] = 8
    m["banane"] = 10  // modification

    // Suppression
    delete(m, "pomme")

    // Parcours
    for fruit, quantite := range m {
        fmt.Printf("%s : %d\n", fruit, quantite)
    }
}
```

---

## 7. Diagramme Mermaid - fonctionnement d'une map  

```mermaid
classDiagram
    class Map {
        +make(type clés, type valeurs)
        +get(clé) valeur, ok
        +set(clé, valeur)
        +delete(clé)
        +range loop: clé, valeur
    }
    Map --> "clé" : indexe
    Map --> "valeur" : contient
```

---

## 8. Points clés  

| Opération       | Syntaxe                 | Notes                              |
|-----------------|------------------------|----------------------------------|
| Déclaration     | `var m map[K]V`         | Initialise à `nil`, inutilisable avant `make`  |
| Initialisation  | `m = make(map[K]V)`     | Crée une map vide utilisable     |
| Ajout/modif     | `m[clé] = valeur`       | Écrase si la clé existe déjà     |
| Accès           | `val, ok := m[clé]`     | `ok` indique si clé existe       |
| Suppression     | `delete(m, clé)`        | Supprime la paire clé-valeur     |
| Parcours        | `for k, v := range m`   | Itère dans un ordre non garanti  |

---

## Sources  

- Go Official Blog, "Maps in Go": https://go.dev/blog/maps  
- Documentation Go, "Maps": https://pkg.go.dev/builtin#map  
- Tour of Go, "Maps": https://go.dev/tour/moretypes/16  
- Go by Example, "Maps": https://gobyexample.com/maps  

---

Ce cours explicite la manipulation des maps, structure clé pour l’association rapide clé-valeur dans Go, indispensable pour organiser et accéder efficacement aux données.