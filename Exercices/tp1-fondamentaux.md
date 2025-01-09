# TP1 - Fondamentaux

<details>

<summary>Commandes Git utiles</summary>

## Commandes de base

```bash
# Initialiser un dépôt
git init

# Vérifier l'état des fichiers
git status

# Ajouter des fichiers au staging
git add nom_du_fichier    # Un fichier spécifique
git add .                 # Tous les fichiers modifiés

# Créer un commit
git commit -m "Message du commit"
```

## Gestion des fichiers

```bash
# Supprimer un fichier
git rm nom_du_fichier

# Annuler des modifications
git restore nom_du_fichier                    # Annule les modifications locales
git restore --source hash_commit nom_du_fichier

# HEAD représente le commit en cours
# HEAD~1 représente le commit parent
# HEAD~2 représente le parent du parent, etc.
git restore --source HEAD~1 nom_du_fichier    # Restaure depuis le commit parent
```

## Explorer et comparer

```bash
# Afficher l'historique
git log                     # Historique détaillé
git log --oneline          # Format condensé
git log --oneline --graph  # Avec représentation graphique

# Comparer des versions
git diff                              # Modifications non stagées
git diff hash_commit1 hash_commit2    # Entre deux commits
```

</details>

## Créez et gérez votre collection préférée avec Git

### Objectif

Créer une collection personnelle (jeux vidéo, musiques, ou films) en utilisant les commandes Git pour gérer et suivre les modifications. L'exercice couvre la création, la modification, la suppression de fichiers et la validation des étapes.

### Thèmes au choix

- **Jeux vidéo** : Collection de jeux préférés, classés par console ou genre
- **Musiques** : Playlist par style de musique
- **Films** : Films préférés par genre

### Instructions

#### Étape 1 : Initialisation

1. Créez un dossier selon le thème choisi :
   - `ma-collection-jeux`
   - `ma-collection-musiques`
   - `ma-collection-films`
2. Initialisez un dépôt Git dans ce dossier

#### Étape 2 : Structuration

1. Créez trois fichiers pour vos catégories (exemples) :
   - Pour jeux vidéo : `console-nintendo.txt`, `console-playstation.txt`, `console-xbox.txt`
   - Pour musiques : `rock.txt`, `pop.txt`, `jazz.txt`
   - Pour films : `science-fiction.txt`, `comedie.txt`, `thriller.txt`
2. Ajoutez ces fichiers au staging
3. Validez avec un message approprié

#### Étape 3 : Ajout des favoris

1. Ajoutez 5 éléments dans chaque fichier
2. Staging et commit pour chaque catégorie (1 commit par catégorie)

#### Étape 4 : Ajout multiple

1. Créez un nouveau fichier (ex: `jeux-independants.txt`)
2. Modifiez un fichier existant (+2 éléments)
3. Staging et commit des modifications (1 seul commit)

#### Étape 5 : Correction d'erreur

1. Introduisez une erreur volontaire dans un fichier
2. Faites un commit de cette erreur avec le message "Ajout avec erreur"
3. Vérifiez l'erreur avec `git diff`
4. Corrigez l'erreur dans le fichier
5. Faites un nouveau commit avec le message "Correction de l'erreur"

#### Étape 6 : Suppression de catégorie

1. Supprimez un fichier de catégorie
2. Staging et commit de la suppression (1 seul commit)

#### Étape 7 : Exploration de l'historique

1. Affichez l'historique complet
2. Consultez le résumé one-line
3. Comparez deux commits
4. Affichez l'historique avec des graphiques

### Exemples de commits attendus

```bash
"Ajout des catégories de jeux vidéo"
"Ajout des jeux Nintendo préférés"
"Ajout des jeux indépendants et mise à jour des jeux PlayStation"
"Correction : suppression d'un film comique mal classé"
"Suppression de la catégorie science-fiction"
```
