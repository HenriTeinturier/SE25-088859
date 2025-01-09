# Workflow Git : Un Exemple Concret

Pour comprendre comment Git fonctionne concrètement, suivons un exemple typique de développement en équipe.

![Workflow Git avec branches](https://wac-cdn.atlassian.com/dam/jcr:34c86360-8dea-4be4-92f7-6597d4d5bfae/02%20Feature%20branches.svg?cdnVersion=2484)

## Les Étapes du Workflow

### 1. Création du Projet Initial

- Création de la version initiale (v0.1)
- La ligne bleue représente la branche principale (`main`)
- C'est la version en production de notre application
- Cette branche contient toujours du code stable et déployable

### 2. Mise en Place de la Branche de Développement

- Création d'une copie de la branche `main` appelée `develop`
- Cette branche servira de base pour développer les nouvelles fonctionnalités
- Elle permet d'isoler le développement de la production

### 3. Distribution du Travail

- Deux développeurs travaillent sur des fonctionnalités différentes
- Chacun récupère une copie complète du projet
  - Historique complet
  - Toutes les branches
  - Configuration du projet

### 4. Développement des Fonctionnalités

- Chaque développeur crée sa propre branche depuis `develop`
- Les développeurs peuvent :
  - Faire plusieurs commits
  - Tester leur code
  - Travailler sans impacter les autres
- Une fois terminé, demande d'intégration vers `develop`

### 5. Intégration et Déploiement

- Fusion des branches de fonctionnalités dans `develop`
- Tests d'intégration
- Si tout est validé, fusion vers `main`
- Attribution d'un nouveau numéro de version
- Déploiement en production

### 6. Avantages de cette Organisation

- Séparation claire entre production et développement
- Possibilité de travailler en parallèle
- Isolation des fonctionnalités
- Processus de validation structuré

### 7. Fonctionnalités Avancées

- Retour possible à n'importe quelle version précédente
- Navigation flexible entre les branches
- Synchronisation avec le dépôt distant :
  - Mise à jour du code (pull)
  - Envoi des modifications (push)
  - Gestion des conflits
  - Travail asynchrone possible

## Pour Aller Plus Loin

Pour une explication détaillée du workflow Gitflow, vous pouvez consulter [la documentation Atlassian](https://www.atlassian.com/fr/git/tutorials/comparing-workflows/gitflow-workflow).
