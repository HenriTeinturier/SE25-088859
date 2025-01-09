# TP2 - Manipulation des commits

<details>
<summary>Commandes Git utiles</summary>

## Navigation et modification

```bash
# Voir l'historique
git log --oneline

# Modifier le dernier commit
git commit --amend -m "message"
git commit --amend --no-edit

# Annuler des modifications
git revert hash_commit
git reset HEAD~1
```

</details>

## Objectif

Créer une page web simple en utilisant les différentes commandes de manipulation des commits.

### Instructions

#### Étape 1 : Structure initiale

1. Créez un dossier `site-portfolio`
2. Initialisez un dépôt Git
3. Créez un fichier `index.html` avec cette structure :

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

4. Commitez avec le message "Structure HTML initiale"

#### Étape 2 : Ajout du contenu principal

1. Dans la section `<main>`, ajoutez :

```html
<section id="about">
  <h2>À propos</h2>
  <p>Développeur passionné par le web</p>
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

#### Étape 3 : Modification avec amend

1. Vous remarquez une faute : "Développeur passioné"
2. Corrigez la faute
3. Utilisez `--amend` pour modifier le dernier commit sans en créer un nouveau

#### Étape 4 : Ajout et annulation

1. Ajoutez une section projets :

```html
<section id="projects">
  <h2>Mes Projets</h2>
  <div class="project">
    <h3>Projet secret</h3>
    <p>Information confidentielle</p>
  </div>
</section>
```

2. Commitez avec le message "Ajout section projets confidentiels"
3. Utilisez `git revert` pour annuler ce commit (les informations ne devaient pas être publiques)

#### Étape 5 : Reset et nouvelle version

1. Ajoutez un style inapproprié dans `<head>` :

```html
<style>
  body {
    background: red;
    color: green;
  }
</style>
```

2. Commitez avec le message "Ajout style temporaire"

3. Vérifiez votre historique, il devrait ressembler à :

```bash
hash (HEAD) Ajout style temporaire
hash Revert "Ajout section projets confidentiels"
hash Ajout section projets confidentiels
hash Ajout sections À propos et Compétences
hash Structure HTML initiale
```

4. Utilisez `git reset HEAD~1` pour annuler ce commit
5. Vérifiez que le commit "Ajout style temporaire" a disparu de l'historique :

```bash
hash (HEAD) Revert "Ajout section projets confidentiels"
hash Ajout section projets confidentiels
hash Ajout sections À propos et Compétences
hash Structure HTML initiale
```

6. Ajoutez un style correct :

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

7. Commitez avec le message "Ajout style définitif"

### Résultat attendu

Votre historique devrait ressembler à :

```bash
hash (HEAD) Ajout style définitif
hash Revert "Ajout section projets confidentiels"
hash Ajout section projets confidentiels
hash Ajout sections À propos et Compétences
hash Structure HTML initiale
```

> 💡 **Note** : Utilisez `git log --oneline` pour vérifier votre historique
