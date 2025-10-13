## **Thème 1 – Types et variables (Exercices 1 à 5)**

### **Exercice 1 — Bonjour Go !**

**Objectif :** Comprendre la structure minimale d’un programme Go.
**Consigne :**
Écris un programme qui affiche le texte :

```
Bonjour, Go !
```

**Indice :** utilise `fmt.Println()` et la fonction `main()`.

---

### **Exercice 2 — Déclaration de variables**

**Objectif :** Déclarer et initialiser des variables de base.
**Consigne :**
Déclare une variable `nom` (string), `age` (int) et `taille` (float64).
Affiche ensuite une phrase complète du type :

```
Je m'appelle Alice, j'ai 20 ans et je mesure 1.65 m.
```

---

### **Exercice 3 — Conversion de types**

**Objectif :** Manipuler la conversion entre types.
**Consigne :**
Demande à l'utilisateur un nombre entier, puis affiche son équivalent en `float64`.
**Indice :** utilise `float64(monInt)`.

---

### **Exercice 4 — Constantes et opérateurs**

**Objectif :** Utiliser les constantes et faire des calculs simples.
**Consigne :**
Déclare une constante `pi = 3.14159` et une variable `rayon = 5.0`.
Calcule et affiche la surface d’un cercle.
**Formule :** `surface = pi * rayon * rayon`.

---

### **Exercice 5 — Lecture clavier**

**Objectif :** Lire une saisie utilisateur.
**Consigne :**
Demande à l’utilisateur son prénom, puis affiche :

```
Bonjour, <prénom> !
```

**Indice :** utilise `fmt.Scan()`.

---

## **Thème 2 – Boucles et conditions (Exercices 6 à 10)**

### **Exercice 6 — Pair ou impair**

**Objectif :** Utiliser une condition simple.
**Consigne :**
Demande un nombre entier à l'utilisateur et indique s’il est pair ou impair.

---

### **Exercice 7 — Maximum de deux nombres**

**Objectif :** Comparer deux valeurs.
**Consigne :**
Demande deux nombres à l'utilisateur, puis affiche le plus grand.

---

### **Exercice 8 — Compteur avec `for`**

**Objectif :** Boucle de base.
**Consigne :**
Affiche les nombres de 1 à 10 sur une ligne, séparés par un espace.

---

### **Exercice 9 — Somme des n premiers entiers**

**Objectif :** Combiner boucle et variables.
**Consigne :**
Demande à l’utilisateur un nombre `n` et calcule la somme de 1 à `n`.

---

### **Exercice 10 — Table de multiplication**

**Objectif :** Boucles imbriquées.
**Consigne :**
Affiche la table de multiplication de 1 à 10.
**Bonus :** aligne les colonnes proprement.

---

## **Thème 3 – Tableaux, slices et maps (Exercices 11 à 15)**

### **Exercice 11 — Tableau fixe**

**Objectif :** Manipuler un tableau.
**Consigne :**
Crée un tableau de 5 entiers. Initialise-le avec les valeurs `[2, 4, 6, 8, 10]` et affiche la somme des éléments.

---

### **Exercice 12 — Slice dynamique**

**Objectif :** Travailler avec les slices.
**Consigne :**
Demande à l’utilisateur combien de notes il souhaite entrer.
Lis ces notes (float64) et calcule la moyenne.

---

### **Exercice 13 — Append et copie**

**Objectif :** Maîtriser la création et la modification d’un slice.
**Consigne :**
Crée un slice `nombres` contenant `[1, 2, 3]`.
Ajoute-y `[4, 5, 6]`, puis affiche le slice complet et sa longueur.

---

### **Exercice 14 — Maps (dictionnaires)**

**Objectif :** Découvrir les maps clé/valeur.
**Consigne :**
Crée une map qui associe un pays à sa capitale (3 pays).
Permets à l’utilisateur de saisir un pays et affiche sa capitale si elle existe.

---

### **Exercice 15 — Comptage des occurrences**

**Objectif :** Utiliser une map pour compter des fréquences.
**Consigne :**
Écris un programme qui compte combien de fois chaque lettre apparaît dans une chaîne donnée.

---

## **Thème 4 – Fonctions (Exercices 16 à 20)**

### **Exercice 16 — Fonction simple**

**Objectif :** Définir et appeler une fonction.
**Consigne :**
Écris une fonction `bonjour(nom string)` qui affiche

```
Bonjour, <nom> !
```

Appelle-la depuis `main()`.

---

### **Exercice 17 — Fonction avec retour**

**Objectif :** Retourner une valeur.
**Consigne :**
Crée une fonction `carre(x int) int` qui retourne le carré de `x`.

---

### **Exercice 18 — Fonction avec plusieurs retours**

**Objectif :** Découvrir les retours multiples.
**Consigne :**
Écris une fonction `divmod(a, b int)` qui retourne à la fois le quotient et le reste de la division entière.

---

### **Exercice 19 — Fonctions variadiques**

**Objectif :** Gérer un nombre variable d’arguments.
**Consigne :**
Crée une fonction `somme(nums ...int)` qui calcule la somme de tous les entiers passés en argument.

---

### **Exercice 20 — Fonctions et slices**

**Objectif :** Passer un slice à une fonction.
**Consigne :**
Écris une fonction `moyenne(notes []float64) float64` qui calcule la moyenne des notes contenues dans le slice.
Teste la fonction dans `main()` avec une liste prédéfinie.

