# Dépannage des problèmes courants avec Git Remote

## Problèmes d'association entre branches

### 1. Problèmes de synchronisation
#### Situation
Quand vous modifiez ou supprimez le lien (upstream) entre une branche locale et distante, plusieurs problèmes peuvent survenir :

#### Cas 1 : Fichiers modifiés non commités
**Problème** : Des fichiers modifiés ou en "staged" lors du changement d'association
```bash
git branch --set-upstream-to=origin/autre-branche ma-branche
```
**Risques** :
- Aucun impact immédiat sur les modifications locales
- Conflits potentiels lors du prochain pull

**Solution** :
1. Committez ou stashez vos modifications avant de changer l'association
```bash
git stash
git branch --set-upstream-to=origin/autre-branche
git stash pop
```

#### Cas 2 : Commits non poussés
**Problème** : Commits locaux non synchronisés lors du changement d'upstream
```bash
fatal: refusing to merge unrelated histories
```

**Solution** :
1. Sauvegardez vos commits
```bash
git branch backup-branch
```
2. Changez l'association
3. Réconciliez les historiques
```bash
git pull --allow-unrelated-histories
# ou
git rebase origin/nouvelle-branche
```

### 2. Problèmes de branches dupliquées

#### Situation : Branches "main" en double
**Problème** : Présence simultanée de :
- Une branche locale `main` non associée
- Une branche distante `origin/main`

**Diagnostic** :
```bash
git branch -vv  # Vérifier les associations
```

**Solutions** :
1. Association de la branche locale
```bash
git branch --set-upstream-to=origin/main main
```
2. Suppression si doublon inutile
```bash
git branch -d main  # Supprime la branche locale
```

## Problèmes spécifiques aux commandes

### Problèmes avec git fetch

#### 1. Mises à jour ignorées
**Problème** : Fetch sans inspection des changements

**Solution** :
```bash
git fetch
git diff main origin/main  # Vérifier les différences
git log --oneline main..origin/main  # Voir les nouveaux commits
```

#### 2. Fetch sans fusion
**Problème** : Accumulation de différences non fusionnées

**Solution** :
```bash
git fetch
git merge origin/main  # ou
git rebase origin/main
```

#### 3. Confusion branches locales/distantes
**Problème** : Mauvaise compréhension des différences local/distant

**Solution** :
```bash
git branch -vv  # Voir les associations et différences
git remote show origin  # Voir l'état détaillé
```

### Problèmes avec git pull

#### 1. Conflits de merge automatique
**Problème** : Fusion automatique créant des conflits

**Solution** : Approche en deux étapes
```bash
git fetch origin
git diff main origin/main  # Vérifier les changements
git merge origin/main      # Fusion contrôlée
```

#### 2. Historique désordonné
**Problème** : Commits de merge automatiques polluant l'historique

**Solution** : Utiliser rebase
```bash
git pull --rebase origin
```

## Bonnes pratiques de prévention

1. Vérifiez toujours l'état avant les opérations
```bash
git status
git branch -vv
```

2. Sauvegardez avant les changements majeurs
```bash
git branch backup-$(date +%Y%m%d)
```

3. Utilisez des alias pour les commandes de vérification
```bash
git config --global alias.state 'status -sb'
git config --global alias.branches 'branch -vv'
```

4. Documentez les associations de branches
```bash
git remote show origin > remote-state.txt
```
