# TP4 - Gestion des Branches et Conflits Git

<details>
<summary>Commandes Git utiles</summary>

```bash
# Gestion des branches
git branch                    # Liste les branches
git switch -c nom-branche    # Crée et bascule sur une nouvelle branche
git switch nom-branche       # Bascule sur une branche existante

# Fusion
git merge nom-branche        # Fusionne nom-branche dans la branche courante

# Vérification
git status                   # État du dépôt
git log --oneline --graph    # Visualise l'historique
```

</details>

## Exercice 1 : Profils et Conflits

### Objectif

Pratiquer la gestion des branches et la résolution de conflits en modifiant des profils d'équipe.

### Prérequis

- Travailler en binôme
- Avoir terminé le TP3
- Avoir Git Graph installé

### Instructions

#### Phase 1 : Enrichissement des profils

1. Chacun crée sa branche de fonctionnalité :

```bash
git switch -c feature/profile-<votre-prenom>
```

2. Dans votre fichier `<prenom>/presentation.md`, ajoutez ces sections :

```markdown
## Compétences techniques

- Languages : (ex: JavaScript, Python, Java...)
- Frameworks : (ex: React, Spring, Laravel...)
- Outils : (ex: VS Code, Git, Docker...)

## Soft Skills

- (ex: Travail d'équipe)
- (ex: Communication)
- (ex: Gestion du temps)

## Centres d'intérêt

- (ex: Développement web)
- (ex: Intelligence artificielle)
- (ex: DevOps)
```

3. Committez et poussez vos modifications

4. Mergez votre branche sur main :
   - Basculez sur la branche main
   - Mettez à jour votre branche main
   - Mergez votre branche de fonctionnalité
   - Poussez les modifications

#### Phase 2 : Création de conflits et résolution

1. Créez une branche de review :

```bash
git switch -c feature/review-<votre-prenom>
```

2. Modifications simultanées :

   - Personne A :

     - Modifiez la section "Compétences techniques" dans VOTRE fichier
     - Ajoutez 3 nouvelles compétences
     - Modifiez la section "Compétences techniques" dans le fichier de B
     - Ajoutez un commentaire : "Suggestion : ajouter SQL aux compétences"

   - Personne B :
     - Modifiez la section "Compétences techniques" dans VOTRE fichier
     - Ajoutez 3 nouvelles compétences
     - Modifiez la section "Compétences techniques" dans le fichier de A
     - Ajoutez un commentaire : "Suggestion : ajouter Docker aux compétences"

3. Chacun commit et push sur sa branche

4. Résolution des conflits :
   - Personne A merge `feature/review-B` dans sa branche
   - Personne B merge `feature/review-A` dans sa branche

## Exercice 2 : Modification Simultanée d'un Fichier Commun

### Objectif

Gérer un conflit sur un fichier partagé.

### Instructions

1. Créez un fichier `team-charter.md` à la racine :

```markdown
# Charte d'équipe

## Nos Valeurs

- Respect
- Collaboration
- Innovation

## Nos Objectifs

- Livrer des features de qualité
- Maintenir un code propre
- Partager les connaissances

## Nos Méthodes

- Daily stand-up
- Code review
- Documentation
```

2. Chacun crée une branche :

```bash
git switch -c feature/charter-<votre-prenom>
```

3. Modifications simultanées :

   - Personne A : Modifie la section "Nos Objectifs"
   - Personne B : Modifie la section "Nos Objectifs"

4. Commit et push

5. Merge des branches et résolution du conflit

### Résultat Attendu

- Avoir expérimenté deux types de conflits différents
- Savoir utiliser Git Graph pour visualiser les branches
- Comprendre le processus de résolution de conflits

> 💡 Conseil : Prenez le temps d'examiner les conflits dans VS Code et discutez avec votre binôme de la meilleure façon de les résoudre.
