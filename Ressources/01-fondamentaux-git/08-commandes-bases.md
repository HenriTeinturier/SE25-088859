# Commandes de base Git

## Gestion des fichiers et staging

```bash
# Vérifier l'état des fichiers
git status

# Ajouter des fichiers au staging
git add nom_du_fichier    # Un fichier spécifique
git add .                 # Tous les fichiers modifiés

# Retirer des fichiers du staging
git restore --staged nom_du_fichier    # Un fichier spécifique
git restore --staged .                 # Tous les fichiers

# Annuler les modifications locales
git restore nom_du_fichier    # Un fichier spécifique
git restore .                # Tous les fichiers
```

## Création des commits

```bash
# Créer un commit
git commit -m "Message du commit"                    # Avec message court
git commit -m "Titre" -m "Description détaillée"     # Avec titre et description
git commit                                           # Ouvre l'éditeur pour le message
```

## Visualisation des différences

```bash
# Voir les différences
git diff                      # Entre working directory et staging
git diff nom_du_fichier      # Pour un fichier spécifique
git diff hash_commit         # Entre working directory et un commit
```

## Historique des commits

```bash
# Afficher l'historique
git log                     # Historique détaillé
git log --oneline          # Format condensé
git log --oneline --graph  # Avec représentation graphique

# Filtrer l'historique
git log -n 5                        # Les 5 derniers commits
git log --since="2023-01-01"       # Depuis une date
git log --author="Nom de l'auteur" # Par auteur
```

> 💡 **Note** : La plupart de ces commandes peuvent être exécutées via l'interface graphique de VS Code dans l'onglet "Source Control" (Ctrl+Shift+G).

## Bonnes pratiques pour les commits

- Utilisez des messages clairs et descriptifs
- Séparez le titre et la description si nécessaire
- Faites des commits atomiques (une fonctionnalité = un commit)
- Vérifiez toujours le contenu avec `git status` avant de commiter
