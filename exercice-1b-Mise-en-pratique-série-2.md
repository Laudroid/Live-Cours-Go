
# Thème – Boucles imbriquées et affichage de motifs

---

### **Exercice 1 — Ligne d’étoiles**

#### **Objectif :**

Découvrir la boucle `for` et la répétition de caractères.

#### **Consigne :**

Écris un programme qui affiche une ligne composée de **10 étoiles** (`*`) :

```
**********
```

#### **Indice :**

Utilise une boucle `for` simple allant de 1 à 10 et affiche `*` sans retour à la ligne après chaque itération.
Astuce : `fmt.Print()` ne saute pas de ligne, contrairement à `fmt.Println()`.

---

### **Exercice 2 — Carré plein d’étoiles**

#### **Objectif :**

Comprendre l’utilisation de **boucles imbriquées**.

#### **Consigne :**

Écris un programme qui affiche un **carré de 10 lignes** et **10 colonnes** d’étoiles :

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

#### **Indice :**

Une boucle extérieure gère les lignes, et une boucle intérieure les colonnes.

---

### **Exercice 3 — Carré vide**

#### **Objectif :**

Manipuler les conditions à l’intérieur des boucles pour créer un motif creux.

#### **Consigne :**

Affiche un carré de 10x10, mais seulement les bords sont remplis d’étoiles :

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

#### **Indice :**

* Les lignes 1 et 10 doivent être pleines.
* Pour les autres lignes, affiche `*` uniquement au début et à la fin.

---

### **Exercice 4 — Triangle plein**

#### **Objectif :**

Utiliser une boucle dépendante d’une autre pour générer une forme triangulaire.

#### **Consigne :**

Écris un programme qui affiche un triangle d’étoiles croissant :

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

#### **Indice :**

La ligne `i` doit contenir `i` étoiles.
Tu peux utiliser une boucle imbriquée : la première gère les lignes, la seconde les étoiles.

---

### **Exercice 5 — Triangle vide**

#### **Objectif :**

Combiner boucles et conditions pour tracer un triangle creux.

#### **Consigne :**

Affiche un triangle vide en étoiles, dont la dernière ligne est complète :

```
*
**
* *
*  *
*   *
*    *
*     *
********
```

#### **Indice :**

* Première et dernière colonne : afficher `*`.
* Intérieur : afficher un espace.
* Dernière ligne : remplir complètement d’étoiles.


