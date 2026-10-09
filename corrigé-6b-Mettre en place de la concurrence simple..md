# Solution 1 : Goroutines avec communication via channel de chaînes

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

// worker simule un travail variable et envoie un message sur le channel
func worker(id int, c chan<- string) {
	fmt.Printf("Worker %d démarre\n", id)

	// Durée aléatoire entre 1 et 3 secondes
	sleepTime := time.Duration(rand.Intn(3)+1) * time.Second
	time.Sleep(sleepTime)

	// Envoyer le message de fin sur le channel
	c <- fmt.Sprintf("Worker %d terminé", id)
}

func main() {
	rand.Seed(time.Now().UnixNano())

	results := make(chan string)
	numWorkers := 5

	// Lancement des goroutines
	for i := 1; i <= numWorkers; i++ {
		go worker(i, results)
	}

	// Récupération et affichage des résultats
	for i := 0; i < numWorkers; i++ {
		msg := <-results
		fmt.Println(msg)
	}
}
```

### Explications

- La fonction `worker` reçoit un `id` et un channel dédié à l’envoi (`chan<- string`).
- Chaque goroutine `worker` effectue une pause aléatoire simulant une tâche, puis envoie un message.
- En `main`, on démarre 5 goroutines qui exécutent `worker`.
- Le channel `results` est utilisé pour recevoir les messages des goroutines.
- La boucle finale dans `main` attend bien 5 messages, assurant que le programme ne termine pas prématurément.
- Pas besoin de fermer le channel car le nombre fixe de messages est connu à l’avance.

---

# Solution 2 : Goroutines retournant un entier, sommation, et utilisation de sync.WaitGroup

```go
package main

import (
	"fmt"
	"math/rand"
	"sync"
	"time"
)

// worker calcule un temps aléatoire, l’envoie sur channel, et signale la fin via WaitGroup
func worker(id int, c chan<- int, wg *sync.WaitGroup) {
	defer wg.Done()

	fmt.Printf("Worker %d démarre\n", id)

	sleepTime := rand.Intn(3) + 1 // secondes
	time.Sleep(time.Duration(sleepTime) * time.Second)

	c <- sleepTime
}

func main() {
	rand.Seed(time.Now().UnixNano())

	numWorkers := 5
	results := make(chan int, numWorkers) // channel bufferisé pour éviter blocage
	var wg sync.WaitGroup

	wg.Add(numWorkers)
	for i := 1; i <= numWorkers; i++ {
		go worker(i, results, &wg)
	}

	// Goroutine distincte pour fermer le channel une fois toutes terminées
	go func() {
		wg.Wait()
		close(results)
	}()

	sum := 0
	for duration := range results {
		fmt.Printf("Reçu temps de pause: %d seconde(s)\n", duration)
		sum += duration
	}
	fmt.Printf("Temps total cumulé: %d secondes\n", sum)
}
```

### Explications

- Ici, `worker` retourne un entier indiquant la durée de la pause.
- Un `sync.WaitGroup` est utilisé pour attendre la fin de toutes les goroutines plutôt que de compter les messages.
- Le channel `results` est bufferisé, ce qui permet d’éviter un blocage si `worker` envoie rapidement.
- Une goroutine anonyme fait `wg.Wait()` puis ferme le channel pour signaler la fin de l’envoi.
- La boucle `for` range sur le channel pour lire tous les résultats, calcule la somme des pauses.
- Cette méthode sépare clairement synchronisation et récupération des résultats avec un code robuste et idiomatique.

---

Ces deux variantes illustrent la puissance des goroutines et channels pour la concurrence en Go, avec des techniques différentes de coordination et collecte des résultats.