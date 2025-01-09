# Initialisation d'un dépôt Git

## Préparation de l'environnement

Pour commencer à travailler avec Git, il faut :

1. Ouvrir un terminal
2. Créer et se placer dans le répertoire du projet
3. Initialiser le dépôt Git

## Commandes de base

```bash
# Créer et accéder au répertoire du projet (exemple)
mkdir mon-projet
cd mon-projet

# Initialiser un nouveau dépôt Git
git init
```

## Le dossier .git

Après l'initialisation, Git crée un dossier caché `.git` à la racine du projet. Ce dossier est crucial car il :

- Contient toute la base de données Git
- Stocke l'historique complet du projet
- Gère les configurations locales du dépôt
- Ne doit **jamais** être modifié manuellement

> ⚠️ La commande `git init` ne doit être exécutée qu'une seule fois, à la racine du projet.

## Branche par défaut

- Après l'initialisation, Git crée automatiquement une branche nommée `main`
- Cette branche est visible dans l'invite de commande : `(main)`
- Si vous voyez `master` au lieu de `main`, c'est que la configuration par défaut n'a pas été mise à jour
