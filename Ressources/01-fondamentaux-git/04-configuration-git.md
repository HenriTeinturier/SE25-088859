# Configuration de Git

Git permet de configurer différentes options à trois niveaux différents :

- **Niveau local** (repository spécifique) : `git config --list`
- **Niveau global** (utilisateur) : `git config --global --list`
- **Niveau système** (tous les utilisateurs) : `git config --system --list`

## Hiérarchie des configurations

Git utilise une hiérarchie de priorité pour les configurations :

1. Configuration locale (plus prioritaire)
2. Configuration globale
3. Configuration système (moins prioritaire)

## Configuration initiale essentielle

Les deux paramètres les plus importants à configurer sont l'identité de l'utilisateur et son email :

```bash
git config --global user.name "Nom d'utilisateur"
git config --global user.email "email@domain.com"
```

## Autres configurations utiles

Voici quelques configurations supplémentaires pratiques :

```bash
# Définir l'éditeur par défaut
git config --global core.editor "nano"  # Utiliser nano comme éditeur

# Définir la branche par défaut
git config --global init.defaultBranch main

# Activer la colorisation de la sortie Git
git config --global color.ui true

# Personnaliser les couleurs
git config --global color.status.changed "yellow"
git config --global color.status.untracked "red"
git config --global color.branch.current "green"
git config --global color.branch.remote "red"

# Configurer les alias pour des commandes fréquentes
git config --global alias.st "status"
git config --global alias.co "checkout"
git config --global alias.br "branch"
git config --global alias.ci "commit"
git config --global alias.lg "log --oneline --graph --decorate"
```

## Visualiser les configurations

Pour voir toutes vos configurations actuelles :

- Configuration locale : `git config --list`
- Configuration globale : `git config --global --list`
- Configuration système : `git config --system --list`

## Supprimer une configuration

Pour supprimer une configuration :

```bash
git config --global --unset nom.parametre
```
