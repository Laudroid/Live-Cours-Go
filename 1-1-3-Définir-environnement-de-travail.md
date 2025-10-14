
## Étape 1 – Installer Go

1. Va sur la page officielle : [https://go.dev/dl/](https://go.dev/dl/)
2. Télécharge le **Windows installer (.msi)** correspondant à ta machine (probablement **amd64**).
3. Lance l’installateur → il va ajouter `go` et `gofmt` à ton **PATH**.
4. Vérifie l’installation dans **PowerShell** ou **cmd** :

   ```bash
   go version
   ```

   Tu dois voir un message du type `go version go1.23.2 windows/amd64`.

---

## Étape 2 – Choisir un IDE / Éditeur

Plusieurs options selon ton style :

* **Visual Studio Code (recommandé)**

  * Installe VS Code : [https://code.visualstudio.com](https://code.visualstudio.com)
  * Ajoute l’extension **Go** officielle (par l’équipe Go).
  * Elle fournit : autocomplétion, refactoring, lint, debug, test.

* **GoLand (JetBrains, payant mais très complet)**

  * Excellente intégration, debugging puissant.
  * Version gratuite dispo pour étudiants.

* **LiteIDE (léger, open-source)**

  * Moins populaire aujourd’hui, mais très simple si tu veux un IDE spécialisé Go.

---

## Étape 3 – Configurer le Debugger

Le débogueur standard pour Go est **Delve**.

* Si tu utilises VS Code, l’extension **Go** installe automatiquement Delve (`dlv`) pour toi.
* Tu pourras alors poser des breakpoints, inspecter les variables et exécuter pas à pas.

---

## Étape 4 – Organisation du Workspace

1. Choisis un dossier de travail, par exemple `C:\Users\TonNom\go`.

2. Vérifie ton GOPATH :

   ```bash
   go env GOPATH
   ```

   Par défaut, c’est `C:\Users\TonNom\go`.

3. Initialise un projet :

   ```bash
   mkdir hello-go
   cd hello-go
   go mod init hello
   ```

   Cela crée un fichier `go.mod`.

4. Ajoute un fichier `main.go` :

   ```go
   package main

   import "fmt"

   func main() {
       fmt.Println("Hello, Go!")
   }
   ```

5. Lance ton programme :

   ```bash
   go run .
   ```

---

## 🛠️ Étape 6 – Outils utiles

* `go fmt` → formatte ton code.
* `go vet` → détecte des erreurs potentielles.
* `golangci-lint` (à installer en plus) → linting avancé.
* `air` (si tu fais du web Go) → rechargement automatique du serveur.

---

👉 Résumé rapide :

* **Compilateur** → fourni avec Go (`go build`, `go run`).
* **IDE** → VS Code + extension Go (ou GoLand si tu veux du full IDE).
* **Debugger** → Delve (intégré avec VS Code).

---
