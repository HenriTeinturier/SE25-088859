# Installation de Git

## Windows

Sur Windows, plusieurs méthodes pour installer Git :

1. **Téléchargement direct :**

   - Visiter [le site officiel de Git](https://git-scm.com/download/windows)
   - Télécharger et exécuter l'installateur
   - Suivre les étapes d'installation en laissant les options par défaut (si besoin).

2. **Installation avec Winget** :

   ```bash
   winget install --id Git.Git -e --source winget
   ```

3. **Installation avec Chocolatey** :

   ```bash
   choco install git
   ```

## macOS et Linux

Sur macOS et Linux, plusieurs options existent pour installer Git :

1. **Utiliser Homebrew (pour macOS) :**

   ```bash
   brew install git
   ```

2. **Installation via le gestionnaire de packages intégré à Linux :**

   - **Debian/Ubuntu :**

     ```bash
     sudo apt update
     sudo apt install git
     ```

   - **Fedora :**

     ```bash
     sudo dnf install git
     ```

   - **Arch Linux :**

     ```bash
     sudo pacman -S git
     ```

3. **Téléchargement et installation depuis les sources (macOS et Linux avancés)** :
   - Télécharger les sources depuis [https://git-scm.com/downloads](https://git-scm.com/downloads).
   - Extraire le fichier et suivre les instructions de compilation indiquées sur le site officiel.

---

Chaque méthode permet d’installer Git de manière standard. Une fois installé, vérifiez l’installation en utilisant la commande suivante :

```bash
git --version
```
