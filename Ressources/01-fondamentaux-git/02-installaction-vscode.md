# Installation VSCode

Suivre l'installation classique de vscode.
[https://code.visualstudio.com/](https://code.visualstudio.com/)

## Différentes parties de VSCode

| Section      | Description                |
| ------------ | -------------------------- |
| Explorer     | Explorateur de fichiers    |
| Recherche    | Recherche globale          |
| Git Contrôle | Gestion de version         |
| Debug        | Débogage                   |
| Extensions   | Marketplace des extensions |

## Configuration de VSCode

### Format on Save

> **Configuration**
>
> - Aller dans `File > Preferences > Settings`
> - Cocher l'option `Format On Save`

## Installation Extensions

### Prettier

1. Installer l'extension Prettier depuis le marketplace
2. Configurer Prettier comme formateur par défaut :
   - Aller dans `File > Preferences > Settings`
   - Rechercher "Default Formatter"
   - Sélectionner "Prettier" dans la liste déroulante

### ESLint

- Installation via le marketplace

## Raccourcis Clavier

### Windows et Linux

| Raccourci        | Action                                                        |
| ---------------- | ------------------------------------------------------------- |
| CTRL + S         | Sauvegarder un fichier (Save)                                 |
| CTRL + Ù         | Ouverture Terminal                                            |
| CTRL + P         | Recherche rapide (Quick Open)                                 |
| CTRL + SHIFT + P | Commande Palette                                              |
| CTRL + Z         | Annuler (Undo)                                                |
| CTRL + Y         | Refaire (Redo)                                                |
| ALT + ↑/↓        | Déplacer une ligne ou sélection vers le haut ou le bas        |
| CTRL + D         | Sélectionner la prochaine occurrence de la sélection courante |

### macOS

| Raccourci       | Action                                                        |
| --------------- | ------------------------------------------------------------- |
| CMD + S         | Sauvegarder un fichier (Save)                                 |
| CMD + T         | Recherche rapide (Quick Open)                                 |
| CMD + SHIFT + P | Commande Palette                                              |
| CMD + Z         | Annuler (Undo)                                                |
| CMD + Y         | Refaire (Redo)                                                |
| CMD + ↑/↓       | Déplacer une ligne ou sélection vers le haut ou le bas        |
| CMD + D         | Sélectionner la prochaine occurrence de la sélection courante |

## Shell Intégré

Sur Windows, le shell intégré est PowerShell.

> **Note :** Possibilité de récupérer bash en installant Git.

Sur macOS, le shell intégré est bash ou zsh selon les versions.  
Sur Linux, le shell intégré est bash pour la plupart des distributions.

Pour lancer vscode à partir d'un terminal dans le dossier courant:

```bash
code .
```
