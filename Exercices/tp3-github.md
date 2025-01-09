# TP3 - Travail collaboratif avec GitHub

<details>
<summary>Commandes Git utiles</summary>

```bash
# Créer et changer de branche
git checkout -b nom-branche

# Vérifier la branche actuelle
git status

# Pousser une nouvelle branche
git push -u origin nom-branche

# Mettre à jour le dépôt local
git fetch
```

</details>

## Objectif

Collaborer sur un projet GitHub en équipe en utilisant les pull requests et le système de review.

### Prérequis

- Avoir un compte GitHub
- Être au moins 2 personnes
- Avoir configuré Git avec SSH

### Instructions

#### Étape 1 : Mise en place (pour le créateur du repo)

1. Créer un nouveau repository sur GitHub
2. Inviter vos collaborateurs (Settings > Collaborators)
3. Cloner le repository en local

#### Étape 2 : Démarrage (pour tous)

1. Cloner le repository

```bash
git clone URL_DU_REPO
```

#### Étape 3 : Création de votre branche

1. Créer et basculer sur une nouvelle branche

```bash
git checkout -b feat/votre-prenom
```

2. Vérifier que vous êtes sur la bonne branche

```bash
git status
```

#### Étape 4 : Ajout de votre présentation

1. Créer un dossier avec votre prénom
2. Créer un fichier `presentation.md` dans ce dossier
3. Commiter ces changements

```bash
git add .
git commit -m "feat: création fichier présentation"
```

#### Étape 5 : Ajout de contenu

1. Dans `presentation.md`, ajouter :
   - Votre nom
   - Votre prénom
   - La date
   - Une personnalité que vous admirez
2. Commiter ces changements

```bash
git commit -m "feat: ajout informations personnelles"
```

#### Étape 6 : Partage du travail

1. Pousser votre branche sur GitHub

```bash
git push -u origin feat/votre-prenom
```

#### Étape 7 : Création de la Pull Request

1. Sur GitHub, créer une Pull Request
2. Base : `main` ← Compare : `feat/votre-prenom`
3. Assigner un reviewer parmi vos collègues
4. Titre : "Présentation de [votre-prenom]"

#### Étape 8 : Review (pour les reviewers)

1. Examiner la Pull Request assignée
2. Ajouter un commentaire demandant plus d'informations sur la personnalité choisie

#### Étape 9 : Modifications suite à la review

1. Ajouter une description de la personnalité dans votre fichier
2. Commiter et pousser les modifications

```bash
git commit -m "feat: ajout description personnalité"
git push
```

#### Étape 10 : Validation finale

1. Le reviewer vérifie les modifications
2. Si tout est bon, approuver la Pull Request
3. Merger la Pull Request

### Structure finale attendue

```
repo/
├── alice/
│   └── presentation.md
├── bob/
│   └── presentation.md
└── charlie/
    └── presentation.md
```

> 💡 Chaque fichier presentation.md doit contenir les informations demandées et la description de la personnalité.
