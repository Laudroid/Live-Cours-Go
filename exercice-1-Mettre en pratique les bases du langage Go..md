
# TP Langage Go : Mini-projet d’interaction basique

## Objectif  
Mettre en pratique les fondamentaux du Go : affichage, lecture utilisateur et variables.

## Énoncé  
Écrire un programme Go qui :  
1. Affiche « Bonjour, Go! »  
2. Demande à l’utilisateur de saisir son nom  
3. Récupère cette saisie  
4. Affiche un message personnalisé du type « Bonjour, [Nom] ! »

## Contraintes et conseils  
- Ne pas utiliser de packages non standards, seule la bibliothèque standard est nécessaire.  
- Pour récupérer l’entrée utilisateur, la fonction `fmt.Scanln()` ou `bufio.NewReader(os.Stdin)` peuvent être utilisées, selon ce que vous préférez et trouvez le plus clair.  
- Testez votre programme dans un terminal ou un outil qui simule la console avec saisie utilisateur.  
- N’hésitez pas à faire appel à l’IA pour vérifier votre syntaxe ou demander un exemple, mais essayez de comprendre les explications fournies et réécrivez le code vous-même.

## Structure possible du programme (indice)  
```go
package main

import (
    "fmt"
)

func main() {
    // Afficher Bonjour, Go!
    
    // Demander le nom
    
    // Lire la saisie
    
    // Afficher le message personnalisé
}
```

## À vous de jouer  
Réalisez ce programme, testez-le, puis essayez de l’améliorer :  
- Que se passe-t-il si l’utilisateur ne saisit rien ?  
- Pouvez-vous ajouter une boucle pour permettre plusieurs saisies sans quitter le programme ?  
- Que faudrait-il modifier pour éviter que l’entrée contienne des espaces en début ou fin ?

---

N’hésitez pas à partager votre code pour un retour ou à poser vos questions.