# Les Commits dans Git

## Qu'est-ce qu'un commit ?

Un commit est une "photographie" (snapshot) de votre projet à un instant T. Il représente :

- L'état complet de tous les fichiers suivis
- Les métadonnées associées (auteur, date, message, etc.)
- Un lien vers le commit parent (historique)

## Structure interne de Git

Git utilise trois types d'objets principaux stockés dans `.git/objects` :

### 1. Blobs (Binary Large Objects)

- Contiennent le contenu des fichiers
- Stockés de manière compressée
- Identifiés par un hash SHA-1
- Ne conservent pas les noms de fichiers

```bash
# Exemple de contenu d'un blob
$ git cat-file -p 83baae61804e65cc73a7201a7252750c76066a30
Hello world!
```

### 2. Trees (Arbres)

- Représentent la structure des répertoires
- Contiennent des références vers :
  - D'autres trees (sous-répertoires)
  - Des blobs (fichiers)
- Stockent les noms de fichiers et les permissions

```bash
# Exemple de structure d'un tree
$ git cat-file -p master^{tree}
100644 blob 83baae61804e65cc73a7201a7252750c76066a30    hello.txt
040000 tree d8329fc1cc938780ffdd9f94e0d364e0ea74f579    docs
```

### 3. Commits

- Pointent vers un tree (état du projet)
- Contiennent des métadonnées :
  - Auteur (nom, email)
  - Date de création
  - Message de commit
  - Hash du commit parent
  - Hash du tree

```bash
# Exemple de structure d'un commit
$ git cat-file -p HEAD
tree a9b3c4d5e6f7...
parent 1b2c3d4e5f6a...
author John Doe <john@example.com> 1623456789 +0200
committer John Doe <john@example.com> 1623456789 +0200

Initial commit
```

## Bonnes pratiques pour les commits

### Messages de commit

- Première ligne : résumé court (50 caractères max)
- Ligne vide
- Description détaillée si nécessaire
- Utiliser le présent ("Add feature" plutôt que "Added feature")

```bash
# Bon exemple de message de commit
git commit -m "Add user authentication feature" -m "
- Implement login/logout functionality
- Add password hashing
- Create user session management
"
```

### Quand commiter ?

- Un commit = une modification logique
- Commiter régulièrement
- Éviter les commits trop gros
- S'assurer que le code compile avant de commiter

### Conventions courantes

- feat: nouvelle fonctionnalité
- fix: correction de bug
- docs: modification de documentation
- style: formatage, point-virgule oublié, etc.
- refactor: refactorisation du code
- test: ajout ou modification de tests

```bash
# Exemples de commits conventionnels
git commit -m "feat: add login page"
git commit -m "fix: correct password validation"
git commit -m "docs: update API documentation"
```

> 💡 **Note** : Les commits sont immuables une fois créés. Bien qu'il soit possible de les modifier avec des commandes avancées, il est préférable de créer de nouveaux commits correctifs.
