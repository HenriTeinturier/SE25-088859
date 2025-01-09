# Correction TP2 - Manipulation des commits

## Étape 1 : Structure initiale

**But** : Créer la structure de base HTML

1. Créez un dossier `site-portfolio` et ouvrez-le dans VS Code
2. Initialisez Git via l'interface VS Code (ou `git init`)
3. Créez `index.html` et copiez cette structure :

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mon Portfolio</title>
  </head>
  <body>
    <header>
      <h1>Mon Portfolio</h1>
    </header>
    <main></main>
    <footer></footer>
  </body>
</html>
```

4. Commitez via VS Code avec le message "Structure HTML initiale"

**Vérification** :

```bash
git log --oneline
# hash Structure HTML initiale
```

## Étape 2 : Ajout du contenu principal

**But** : Ajouter les sections À propos et Compétences

1. Dans VS Code, ajoutez ce contenu entre les balises `<main></main>` :

```html
<section id="about">
  <h2>À propos</h2>
  <p>Développeur passioné par le web</p>
</section>
<section id="skills">
  <h2>Compétences</h2>
  <ul>
    <li>HTML/CSS</li>
    <li>JavaScript</li>
    <li>Git</li>
  </ul>
</section>
```

2. Commitez avec le message "Ajout sections À propos et Compétences"

**Vérification** :

```bash
git log --oneline
# hash Ajout sections À propos et Compétences
# hash Structure HTML initiale
```

## Étape 3 : Modification avec amend

**But** : Corriger une faute sans créer un nouveau commit

1. Corrigez "passioné" en "passionné" dans VS Code
2. Ajoutez la modification au staging
3. Dans le terminal VS Code : `git commit --amend --no-edit`

**Vérification** : L'historique reste identique, seul le contenu est modifié

## Étape 4 : Ajout et annulation

**But** : Ajouter puis annuler du contenu confidentiel avec revert

1. Ajoutez cette section dans `<main>` :

```html
<section id="projects">
  <h2>Mes Projets</h2>
  <div class="project">
    <h3>Projet secret</h3>
    <p>Information confidentielle</p>
  </div>
</section>
```

2. Commitez avec "Ajout section projets confidentiels"
3. Dans le terminal : `git revert HEAD`

**Vérification** :

```bash
git log --oneline
# hash Revert "Ajout section projets confidentiels"
# hash Ajout section projets confidentiels
# hash Ajout sections À propos et Compétences
# hash Structure HTML initiale
```

## Étape 5 : Reset et nouvelle version

**But** : Supprimer un commit avec reset et ajouter une meilleure version

1. Ajoutez ce style dans `<head>` :

```html
<style>
  body {
    background: red;
    color: green;
  }
</style>
```

2. Commitez "Ajout style temporaire"

**Vérification avant reset** :

```bash
git log --oneline
# hash Ajout style temporaire
# hash Revert "Ajout section projets confidentiels"
# hash Ajout section projets confidentiels
# hash Ajout sections À propos et Compétences
# hash Structure HTML initiale
```

3. Dans le terminal : `git reset HEAD~1`

**Vérification après reset** :

```bash
git log --oneline
# hash Revert "Ajout section projets confidentiels"
# hash Ajout section projets confidentiels
# hash Ajout sections À propos et Compétences
# hash Structure HTML initiale
```

4. Ajoutez ce style dans `<head>` :

```html
<style>
  body {
    font-family: Arial, sans-serif;
  }
  header {
    background: #f4f4f4;
    padding: 1em;
  }
</style>
```

5. Commitez "Ajout style définitif"

**Vérification finale** :

```bash
git log --oneline
# hash Ajout style définitif
# hash Revert "Ajout section projets confidentiels"
# hash Ajout section projets confidentiels
# hash Ajout sections À propos et Compétences
# hash Structure HTML initiale
```

> 💡 **Note** : Toutes les modifications de fichiers peuvent être faites directement dans VS Code. Seules les commandes `--amend`, `revert` et `reset` nécessitent le terminal.
