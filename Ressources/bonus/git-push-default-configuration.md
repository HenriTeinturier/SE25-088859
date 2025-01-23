# Configuration de Git push.default : Comprendre et personnaliser le comportement de push

## Configuration automatique des branches distantes
Si tu veux que Git configure automatiquement une branche distante dès le premier git push sans avoir à ajouter --set-upstream chaque fois, tu peux ajuster le comportement global avec cette commande :
```bash
git config --global push.default current
```

## Comprendre push.default

### Qu'est-ce que push.default ?
push.default est une configuration de Git qui contrôle comment les branches locales sont poussées vers le dépôt distant lorsque tu fais un simple git push, sans préciser explicitement la branche ou le remote.

### Comportement de push.default = current
Quand push.default est défini sur current, Git essaie de pousser la branche locale actuelle (active) vers une branche distante portant le même nom.

#### Exemple pratique
Tu es sur une branche locale appelée nouvelle-branche :
```bash
git checkout nouvelle-branche
git push
```

Avec push.default = current :
- Si une branche distante du même nom existe déjà, Git pousse les commits locaux vers cette branche
- Si aucune branche distante du même nom n'existe, Git en crée automatiquement une et l'associe à la branche locale

### Valeurs possibles de push.default

| Valeur | Comportement |
|--------|--------------|
| current | Pousse uniquement la branche locale active vers une branche distante du même nom (ou la crée). |
| matching | Pousse toutes les branches locales qui ont un nom correspondant à une branche distante. |
| upstream | Pousse uniquement les branches locales configurées pour suivre une branche distante. |
| simple (par défaut) | Pousse uniquement la branche actuelle, mais seulement si elle suit une branche distante. Donne une erreur sinon. |
| nothing | Ne pousse rien (comportement totalement désactivé). |

## Avantages et inconvénients

### Avantages
- Facilité d'utilisation pour les nouvelles branches
- Plus besoin de faire git push -u pour configurer l'upstream
- Workflow simplifié pour les développeurs
- Réduction des erreurs liées à l'oubli du -u

### Inconvénients
- Moins explicite (risque de branches inutiles sur le remote)
- Pas toujours recommandé pour les équipes avec des workflows stricts

## Cas d'usage recommandés
push.default = current est recommandé quand :
- Tu travailles principalement en solo ou dans de petites équipes
- Tu veux simplifier le workflow pour pousser rapidement de nouvelles branches
- Tu n'as pas besoin d'un contrôle strict sur la création des branches distantes

À éviter quand :
- Tu travailles avec une équipe qui suit des conventions de nommage strictes
- Tu utilises des workflows spécifiques (comme GitFlow)
