# TP Bonus - Le Restaurant Git

<details>
<summary>Workflow et règles de base</summary>

### Workflow Git

- Toujours créer une branche pour chaque nouvelle fonctionnalité
- Ne jamais travailler directement sur `main`
- Faire valider ses modifications via Pull Request
- Merger uniquement après validation

### Conventions de nommage

```bash
# Branches
# Format général : type/contexte-description

# Pour les profils du staff
staff/ajout-jean            # Ajout du profil de Jean
staff/update-marie          # Mise à jour du profil de Marie

# Pour la carte du restaurant
carte/entree-salade        # Ajout d'une salade en entrée
carte/plat-burger         # Ajout d'un burger en plat
carte/dessert-tiramisu    # Ajout d'un tiramisu en dessert
carte/boisson-mojito      # Ajout d'un mojito aux boissons

# Pour les menus composés
menu/midi-vegetarien      # Menu végétarien du midi
menu/soir-gourmet        # Menu gourmet du soir
menu/special-noel        # Menu spécial pour Noël

# Pour les commandes
order/table-12           # Commande pour la table 12
order/emporter-15        # Commande à emporter n°15

# Pour les fonctionnalités bonus
feature/promo-jour       # Système de promotion
feature/avis-clients     # Système d'avis

# Commits
feat: ajout de [...]     # Nouvelle fonctionnalité
fix: correction de [...]  # Correction d'un bug
docs: mise à jour de [...] # Documentation
```

### Commandes Markdown essentielles

```markdown
# Titre niveau 1

## Titre niveau 2

**Gras**
_Italique_

- Liste à puces

1. Liste numérotée
   [Texte du lien](url)
   ![Texte alternatif](url_image)
```

</details>

## Objectif

Créer un restaurant virtuel collaboratif en utilisant Git et GitHub. Cet exercice peut être réalisé seul ou en équipe.

## Structure du projet

```
restaurant/
├── staff/                  # Profils des cuisiniers
├── menu/
│   ├── entrees/
│   ├── plats/
│   ├── desserts/
│   └── boissons/
├── orders/                 # Commandes des clients
└── README.md              # Présentation du restaurant
```

## Partie 1 : Constitution de l'équipe

### Création de votre profil

1. Créez une branche pour votre profil

```bash
git switch -c feature/staff-[votre-prenom]
```

2. Créez votre fichier `staff/[prenom].md` avec :

```markdown
# [Prénom Nom]

![Photo de profil](url_image)

## À propos

[Votre description créative]

## Rôle

[Chef, Sous-chef, Pâtissier...]

## Spécialités

- [Spécialité 1]
- [Spécialité 2]
- [Spécialité 3]

## Contact

- GitHub : [votre-profil]
- Portfolio : [votre-site]
```

3. Créez une Pull Request pour intégrer votre profil

## Partie 2 : Développement du menu

### Ajout d'un plat

1. Créez une branche pour votre plat

```bash
git switch -c feature/menu-[categorie]-[nom-plat]
```

2. Créez votre fichier dans le dossier approprié :

```markdown
# [Nom du plat]

![Photo du plat](url_image)

## Ingrédients

- [Liste des ingrédients]

## Préparation

1. [Étapes de préparation]

## Chef

Créé par [@votre-prenom]

## Prix

[XX.XX] €
```

### Création d'un menu

1. Créez une branche pour votre menu

```bash
git switch -c feature/menu-special-[nom]
```

2. Composez votre menu en référençant les plats existants

## Partie 3 : Système de commandes

### Prise de commande

1. Créez une branche pour votre commande

```bash
git switch -c feature/order-[numero]
```

2. Ajoutez votre commande dans `orders/[date].md`

```markdown
# Commande #[numero]

Client : [nom]
Heure : [hh:mm]

## Articles

- [plat 1]
- [plat 2]
  ...

Total : [XX.XX] €
```

## Bonus suggérés

- Implémenter un système de réservation

> 💡 **Conseils** :
>
> - Vérifiez toujours que votre branche est à jour avant de commencer
> - Faites des commits atomiques et bien nommés
> - Testez vos fichiers Markdown avant de les soumettre
> - Communiquez avec votre équipe si vous travaillez à plusieurs

### Résultat attendu

- Une équipe de cuisine constituée
- Un menu varié avec des plats détaillés
- Un système de commande fonctionnel
- Une utilisation maîtrisée de Git et GitHub

## Bonus : Système de réservation

### Objectif

Gérer des réservations multiples dans des fichiers partagés en gérant les conflits potentiels.

### Structure

```
restaurant/
└── reservations/
    └── YYYY-MM-DD.md    # Un fichier par date
```

### Template de réservation

```markdown
# Réservations du [DATE]

## Service du midi

### 12h00

- [NOM] ([X] personnes)

### 12h30

- [NOM] ([X] personnes)

## Service du soir

### 19h00

- [NOM] ([X] personnes)

### 19h30

- [NOM] ([X] personnes)
```

### Liste des réservations à gérer

**Pour le 20 mars 2024**

- THOMAS (4 personnes) - 12h00
- ROBERT (2 personnes) - 12h30
- RICHARD (6 personnes) - 12h00
- SIMON (3 personnes) - 12h30
- MICHEL (5 personnes) - 19h00
- LAURENT (2 personnes) - 19h30
- MOREAU (4 personnes) - 19h00
- GARCIA (6 personnes) - 19h30
- DUBOIS (2 personnes) - 12h00
- MARTIN (4 personnes) - 12h30
- PETIT (3 personnes) - 19h00
- DURAND (5 personnes) - 19h30
- LEROY (2 personnes) - 12h00
- ROUX (6 personnes) - 12h30
- GIRARD (4 personnes) - 19h00
- DAVID (3 personnes) - 19h30

**Pour le 21 mars 2024**

- BERNARD (4 personnes) - 12h00
- MOREAU (2 personnes) - 12h30
- FOURNIER (6 personnes) - 12h00
- LAMBERT (3 personnes) - 12h30
- FONTAINE (5 personnes) - 19h00
- ROUSSEAU (2 personnes) - 19h30
- VINCENT (4 personnes) - 19h00
- MULLER (6 personnes) - 19h30
- LEFEVRE (2 personnes) - 12h00
- FAURE (4 personnes) - 12h30
- ANDRE (3 personnes) - 19h00
- MERCIER (5 personnes) - 19h30
- BLANC (2 personnes) - 12h00
- GUERIN (6 personnes) - 12h30
- BOYER (4 personnes) - 19h00
- GARNIER (3 personnes) - 19h30

### Instructions

1. **Première personne** : Créer le fichier template pour une nouvelle date

```bash
git switch -c resa/init-21-mars
# Créer reservations/2024-03-21.md avec le template
git add reservations/2024-03-21.md
git commit -m "resa: init fichier 21 mars"
git push
```

2. **Chaque participant** : Ajouter 3 réservations

```bash
# Créer une branche pour vos 3 réservations
git switch -c resa/20-mars-lot1

# Ajouter 3 réservations de la liste dans le fichier
# Vérifier qu'elles ne sont pas déjà présentes !

git add reservations/2024-03-20.md
git commit -m "resa: ajout 3 réservations pour le 20/03"
git push
```

3. **Gestion des conflits**

- Si d'autres ont modifié le fichier pendant ce temps :

```bash
git fetch
git rebase origin/main
# Résoudre les conflits si nécessaire
git push --force-with-lease
```

> 💡 **Conseils** :
>
> - Vérifiez toujours les réservations existantes avant d'en ajouter
> - Une même personne ne peut pas être à deux endroits en même temps
> - Gérez les conflits en communiquant avec l'équipe
> - Faites valider vos modifications via Pull Request
