# Git : Comprendre les interactions avec les dépôts distants

## Concepts essentiels sur les branches et le remote
a. Une branche locale n'est pas automatiquement liée à une branche distante
Quand tu crées une branche en local avec :
```bash
git checkout -b nouvelle-branche
```

Elle n'est pas automatiquement associée à une branche sur le remote.

C'est seulement après un git push -u que l'association est créée. Si ce n'est pas fait, la branche locale reste indépendante.

b. Vérification des branches et de leur suivi
Pour voir quelles branches locales sont liées à des branches distantes, utilise :
```bash
git branch -vv
```
Cela montre les branches locales et leur remote de suivi (s'il existe).

c. Suppression des branches "orphelines"
Parfois, il peut y avoir des branches qui n'ont plus de correspondant sur le remote. Pour les repérer et nettoyer :

Afficher toutes les branches locales :
```bash
git branch
```
Supprimer les branches locales orphelines :
```bash
git remote prune origin
```

## Création et association d'une branche avec git push

Lorsque vous créez une nouvelle branche locale, elle n'est pas automatiquement liée au dépôt distant. Voici les deux façons de gérer cette situation :

### Cas 1 : Avec l'option -u (recommandé)
```bash
git push -u origin nom-de-la-branche
```

Cette commande effectue deux actions :
1. Crée la branche sur le dépôt distant (origin/nom-de-la-branche)
2. Établit une association de suivi (tracking) entre votre branche locale et la branche distante

L'option `-u` (ou `--set-upstream`) crée une relation parent-enfant entre les branches :
- La branche distante devient la branche "upstream" (parent)
- Votre branche locale devient la branche "downstream" (enfant)

Avantages de cette association :
- Permet d'utiliser `git push` et `git pull` sans arguments supplémentaires
- Facilite le suivi des différences entre les branches (ahead/behind)
- Simplifie la synchronisation des modifications

### Cas 2 : Sans l'option -u
```bash
git push origin nom-de-la-branche
```

Dans ce cas :
- La branche est créée sur le dépôt distant
- Aucune association de suivi n'est établie

Conséquences :
- Pour chaque `git pull`, vous devrez spécifier :
  ```bash
  git pull origin nom-de-la-branche
  ```
- Pour chaque `git push`, vous devrez spécifier :
  ```bash
  git push origin nom-de-la-branche
  ```

## Configuration des remotes
remote origin est le remote par défaut de git pour les nouveaux dépôts.
on peut le voir avec la commande git remote -v

```bash
git remote -v
```

on peut configurer plusieurs remote avec la commande git remote add
```bash
git remote add nom-du-remote chemin-ou-url-du-remote
```

on peut voir le remote attaché à une branche avec la commande git branch -vv

```bash
git branch -vv
```

## Commandes utiles pour la gestion des branches

#### Gestion des associations entre branches
| Commande | Description | Cas d'utilisation |
|----------|-------------|-------------------|
| `git branch --set-upstream-to=origin/nouvelle-branche` | Associe votre branche locale avec une branche distante existante | Quand vous avez créé une branche sans `-u` et souhaitez l'associer après coup |
| `git branch -vv` | Affiche l'état détaillé de toutes vos branches locales et leurs associations | Pour vérifier : <br>- Quelles branches sont associées<br>- Combien de commits d'avance/retard vous avez |

#### Exemples d'utilisation

Pour associer une branche locale existante avec sa distante :
```bash
git branch --set-upstream-to=origin/nouvelle-branche
```
Cette commande est utile quand :
- Vous avez oublié le `-u` lors du premier push
- Vous voulez changer l'association d'une branche

Pour vérifier l'état de vos branches :
```bash
git branch -vv
```
La sortie vous montrera :
- Les branches locales et leurs associations distantes
- Le nombre de commits d'avance (`ahead`) ou de retard (`behind`)
- Les branches sans association (non trackées)

## Commandes d'interaction avec le remote

### Git fetch
Git fetch est une commande fondamentale qui permet de :
1. Récupérer les commits de la branche distante
2. Mettre à jour les références locales des branches distantes
3. Ne pas modifier vos branches locales

#### Fonctionnement détaillé
```bash
git fetch        # Récupère les mises à jour de tous les remotes
git fetch origin # Récupère uniquement les mises à jour du remote origin
```

Quand vous exécutez git fetch, Git :
1. Se connecte au dépôt distant
2. Télécharge les nouveaux commits non présents en local
3. Met à jour les références distantes locales (ex: origin/main)
4. Ne modifie pas vos branches locales

Pour voir les différences après un fetch :
```bash
git diff main origin/main  # Compare votre branche locale avec la distante
```

### Git pull
Git pull combine deux opérations :
1. `git fetch` : récupère les commits distants
2. `git merge` : fusionne ces commits dans votre branche locale

#### Comportement important
- Seule la branche distante associée à votre branche locale est concernée
- Les autres branches distantes ne sont pas impactées
- Un merge automatique est effectué (peut créer des conflits)

```bash
git pull                     # Pull depuis la branche associée
git pull origin main        # Pull spécifiquement depuis origin/main
git pull --rebase origin    # Pull en utilisant rebase au lieu de merge
```

### Comparaison fetch vs pull

| Aspect | Git Fetch | Git Pull |
|--------|-----------|----------|
| Récupération des commits | Oui | Oui |
| Modification branche locale | Non | Oui |
| Risque de conflits | Non | Oui |
| Contrôle | Total | Automatique |
| Cas d'usage | Inspection avant fusion | Mise à jour rapide |

#### Quand utiliser fetch ?
- Pour inspecter les changements avant de les fusionner
- Pour éviter les conflits automatiques
- Quand vous avez des modifications locales non commitées
- Pour plus de contrôle sur le processus de fusion

#### Quand utiliser pull ?
- Pour une mise à jour rapide de votre branche
- Quand vous êtes sûr qu'il n'y aura pas de conflits
- Dans un workflow simple avec peu de risques de conflits

```bash
git fetch origin
git diff main origin/main
```
Cela te montre les différences entre ta branche locale main et origin/main.
Quand tu veux éviter des conflits automatiques :
Avec git fetch, tu peux gérer manuellement les conflits si nécessaire, plutôt que de laisser Git faire un merge automatique (comme avec git pull).
Quand tu travailles sur une branche sensible :
Si tu travailles sur une branche avec des modifications non commit, git fetch est plus sûr car il ne tentera pas de fusionner quoi que ce soit.
