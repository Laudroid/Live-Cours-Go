# Corrigé Détaillé du QCM - Langage Go

---

## Séance 1 : Introduction au Go & Bases du langage

### Question 1
**Réponse correcte : B) La simplicité, la rapidité de compilation et la concurrence native**
- **Explication :** Go a été conçu par Google pour offrir un langage simple à apprendre, avec un temps de compilation très court et une gestion efficace de la concurrence grâce aux *goroutines* et aux *channels*.

### Question 2
**Réponse correcte : A) `x := 10`**
- **Explication :** L'opérateur court `:=` permet de déclarer et d'initialiser une variable en laissant le compilateur inférer son type. `var x int = 10` est également valide mais n'utilise pas l'inférence courte. `let` et `auto` n'existent pas en Go.

### Question 3
**Réponse correcte : C) `for`**
- **Explication :** En Go, `for` est l'unique mot-clé pour effectuer des boucles. Il remplace à la fois les boucles `for` classiques, les boucles `while` (`for condition { ... }`) et les boucles infinies (`for { ... }`).

### Question 4
**Réponse correcte : B) `""` (chaîne vide)**
- **Explication :** En Go, chaque type a une *zero value* attribuée à la déclaration sans initialisation. Pour `string`, c'est `""` ; pour les types numériques, c'est `0` ; et pour les pointeurs/slices/maps, c'est `nil`.

### Question 5
**Réponse correcte : B) `if x > 0 { ... }`**
- **Explication :** En Go, les parenthèses autour de la condition d'un `if` ne sont pas nécessaires (et déconseillées), mais les accolades `{}` autour du bloc d'instructions sont obligatoires.

### Question 6
**Réponse correcte : D) `fmt.Scan()`**
- **Explication :** Le package standard `fmt` fournit la fonction `Scan()` (ainsi que `Scanln` et `Scanf`) pour lire des entrées formatées depuis la saisie utilisateur.

---

## Séance 2 : Collections, fonctions et erreurs

### Question 7
**Réponse correcte : A) La taille d'un tableau est fixe à la compilation, tandis que celle d'une slice est dynamique.**
- **Explication :** Un tableau (`[5]int`) a une taille fixe faisant partie de son type. Une *slice* (`[]int`) est une vue dynamique sur un tableau sous-jacent dont la taille peut évoluer.

### Question 8
**Réponse correcte : D) `append()`**
- **Explication :** La fonction intégrée `append(slice, elements...)` permet d'ajouter des éléments à une slice. Elle réalloue de la mémoire si la capacité de la slice est dépassée et retourne la slice mise à jour.

### Question 9
**Réponse correcte : B) `m := make(map[string]int)`**
- **Explication :** La fonction `make()` est utilisée pour allouer et initialiser des types dynamiques comme les maps et les slices. La déclaration `var m map[int]string` crée une map `nil` non utilisable pour l'écriture sans initialisation.

### Question 10
**Réponse correcte : B) Si la clé existe effectivement dans la map**
- **Explication :** C'est l'idiome *comma ok*. Si la clé existe, `ok` vaut `true`. Si elle n'existe pas, `ok` vaut `false` et `val` prend la *zero value* du type de valeur.

### Question 11
**Réponse correcte : C) Une fonction peut déclarer et retourner plusieurs valeurs de types différents.**
- **Explication :** Go prend nativement en charge le retour multiple (ex: `func div(a, b float64) (float64, error)`), ce qui est notamment très utilisé pour retourner un résultat accompagné d'une erreur.

### Question 12
**Réponse correcte : A) Une fonction anonyme qui capture et référence des variables situées en dehors de son propre corps**
- **Explication :** Une *closure* (ou fermeture) est une fonction anonyme qui conserve l'accès aux variables du contexte dans lequel elle a été créée, même après la fin de ce contexte.

### Question 13
**Réponse correcte : B) En retournant explicitement une valeur de type `error` comme dernière valeur de retour**
- **Explication :** Go n'utilise pas de système d'exceptions `try/catch`. Les erreurs sont traitées comme des valeurs normales renvoyées par les fonctions et vérifiées explicitement (`if err != nil`).

### Question 14
**Réponse correcte : C) `nil`**
- **Explication :** `error` est une interface en Go. La valeur par défaut (*zero value*) d'une interface non initialisée ou représentant l'absence d'erreur est `nil`.

---

## Séance 3 : Structures, pointeurs et organisation du code

### Question 15
**Réponse correcte : B) `type Personne struct { Nom string }`**
- **Explication :** En Go, les structures sont définies avec la syntaxe `type NomStructure struct { ... }`. Il n'y a pas de mot-clé `class` en Go.

### Question 16
**Réponse correcte : A) `func (p Personne) Saluer() { ... }`**
- **Explication :** Les méthodes sont associées à un type grâce à un *receveur* (ici `(p Personne)`) placé entre le mot-clé `func` et le nom de la fonction.

### Question 17
**Réponse correcte : B) `&`**
- **Explication :** L'opérateur d'adresse `&` placé devant une variable (ex: `&x`) permet d'obtenir un pointeur contenant l'adresse mémoire de cette variable.

### Question 18
**Réponse correcte : C) `*p`**
- **Explication :** Placer l'astérisque `*` devant une variable de type pointeur permet d'accéder ou de modifier la valeur stockée à l'adresse mémoire pointée.

### Question 19
**Réponse correcte : D) En faisant commencer son nom par une lettre majuscule**
- **Explication :** La visibilité d'un identifiant en Go dépend uniquement de sa casse : un nom commençant par une majuscule est exporté (public), tandis qu'un nom commençant par une minuscule est privé au package.

### Question 20
**Réponse correcte : A) `go.mod`**
- **Explication :** Le fichier `go.mod` (créé via `go mod init`) définit le chemin du module, la version de Go utilisée ainsi que les dépendances du projet et leurs versions.