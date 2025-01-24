# Git fetch, Pull et Stratégies de Fusion

## Situation initiale
- Branche locale b : A → B → C → D → E
- Branche distante b : A → B → C → F → G

Tu es sur la branche locale b, et lorsque tu fais un git pull, voici ce qui peut se passer selon le type de fusion effectué par Git.

## Cas 1 : Fusion classique (merge)
Lors du git pull, Git récupère les commits distants F et G.
Git détecte que les branches ont divergé après le commit C :
- Branche locale : D → E
- Branche distante : F → G

Pour intégrer les changements, Git crée un commit de fusion (merge commit), que nous appellerons H.

### Ordre des commits dans l'historique
L'historique inclura tous les commits (D, E, F, G) suivis du commit de fusion H. L'ordre ne sera pas strictement linéaire, car un commit de fusion introduit une structure de graphe.

Voici l'évolution de l'historique pendant le processus de fusion :

1. État initial :
```mathematica
Remote: A → B → C → F → G
Local:  A → B → C → D → E
```

2. Après le merge (git pull) :
```mathematica
Remote: A → B → C → F → G
Local:  A → B → C → F → G → H ← E ← D
```

3. Après le push :
```mathematica
Remote: A → B → C → F → G → H ← E ← D
Local:  A → B → C → F → G → H ← E ← D
```

Le commit de fusion H est créé en utilisant :
- L'ancêtre commun C (pour la fusion à trois voies)
- L'état final de la branche distante (G)
- L'état final de la branche locale (E)

Dans un outil comme git log --graph, cela apparaîtra sous forme de graphe avec une branche fusionnée.

## Cas 2 : Fetch puis merge manuel
Avec git fetch, le processus est divisé en deux étapes distinctes :

1. État après le fetch :
```mathematica
Remote: A → B → C → F → G
Local:  A → B → C → D → E
origin/main: A → B → C → F → G
```
Le fetch met à jour la référence origin/main (copie locale de la branche distante) sans modifier votre branche locale.

2. Vous pouvez alors :
- Examiner les changements : `git diff main origin/main`
- Voir les nouveaux commits : `git log main..origin/main`
- Choisir comment intégrer les changements :
  - Soit faire un merge : `git merge origin/main` (même résultat que pull)
  - Soit faire un rebase : `git rebase origin/main` (réécriture de l'historique)

L'avantage du fetch est qu'il vous permet de voir les changements avant de décider comment les intégrer, contrairement au pull qui fait le merge automatiquement.

Dans un outil comme git log --graph, cela apparaîtra sous forme de graphe avec une branche fusionnée.

## Cas 3 : Rebase au lieu de fusion
Si tu utilises git pull --rebase (ou si ton Git est configuré pour rebaser automatiquement lors d'un pull), voici ce qui se passe :
- Git récupère les commits distants F et G
- Git rejoue tes commits locaux D et E par-dessus F → G

### Ordre des commits dans l'historique
L'historique sera complètement linéaire, avec tes commits locaux D et E appliqués après F et G :

```mathematica
A → B → C → F → G → D → E
```

Dans ce cas :
- Il n'y a pas de commit de fusion
- L'ordre des commits dans l'historique est clair et linéaire

## Résumé
- Fusion classique (merge) : Il y a un commit de fusion H qui relie les deux branches. L'historique est sous forme de graphe.
- Rebase (rebase) : Les commits locaux sont rejoués sur la branche distante, et l'historique est linéaire sans commit de fusion.

Si tu veux un historique clair et linéaire, utilise le rebase. Si tu préfères préserver l'historique des branches, utilise la fusion classique.

## Gestion des conflits lors d'un rebase
Lors d'un rebase, si des conflits surviennent, tu dois les résoudre manuellement. Les résolutions de conflits sont automatiquement enregistrées sous forme de nouveaux commits si tu utilises git rebase --continue.

### Contexte initial (Rebase avec conflit)
- Historique distant : A → B → C → F → G
- Historique local : A → B → C → D → E

### Étapes lors d'un rebase avec conflits
1. Rebase commence :
   - Git applique F → G (aucun conflit ici, car ce sont les commits distants)
   - Puis Git tente d'appliquer D

2. Conflit détecté dans D :
   - Tu résous manuellement le conflit
   - Après résolution, tu fais un git rebase --continue
   - Cela crée un nouveau commit pour la version modifiée de D

3. Rebase continue avec E :
   - Git tente d'appliquer E
   - Si un conflit est détecté dans E, même processus :
     - Résolution manuelle
     - Commit de résolution créé après git rebase --continue

### Ordre des commits dans l'historique (avec conflits résolus)
L'historique linéaire résultant ressemblera à ceci :

```mathematica
A → B → C → F → G → D' → E'
```

- F et G : commits distants
- D' : une version modifiée de D, incluant les résolutions de conflit
- E' : une version modifiée de E, incluant les résolutions de conflit

Les commits originaux D et E ne sont plus visibles car ils ont été remplacés par D' et E'.

### Détails des commits de résolution
Les commits D' et E' sont créés automatiquement par Git lors du rebase. Ils incluent :
- Le contenu original de D ou E
- Les modifications nécessaires pour résoudre les conflits

Ces commits remplacent leurs versions originales et s'intègrent dans l'historique linéaire après F → G.

Si tu veux voir ces commits dans ton historique, utilise la commande suivante :

```mathematica
git log --oneline
```

## Retrouver les commits originaux
Oui, il est possible de retrouver les commits originaux D et E après un rebase grâce au reflog.

### Comment fonctionne le Reflog ?
Le reflog enregistre les mouvements de HEAD dans le dépôt, y compris l'un rebase. Même si les commits D et E ne font plus partie de l'historique linéaire après le rebase (remplacés par D' et E'), ils existent toujours dans la base de données Git tant qu'ils n'ont pas été supprimés par le processus de nettoyage automatique (garbage collection).

### Retrouver les commits originaux dans le Reflog
Afficher le Reflog : Exécute la commande suivante pour voir l'historique des mouvements de HEAD :

```mathematica
git reflog
```

Tu verras une sortie similaire à ceci :

```mathematica
d2f8e12 HEAD@{0}: rebase: E'
a1c3f45 HEAD@{1}: rebase: D'
87abc34 HEAD@{2}: checkout: moving from branch to b
65def67 HEAD@{3}: commit: E
23bca89 HEAD@{4}: commit: D
```

Ici :
- 65def67 est le hash du commit E original
- 23bca89 est le hash du commit D original
- d2f8e12 et a1c3f45 sont les nouveaux commits D' et E' créés par le rebase

Pour inspecter un commit :

```mathematica
git show <hash>
```

Pour restaurer un commit (par exemple, recréer une branche) :

```mathematica
git checkout -b old-branch <hash>
```

Exemple :

```mathematica
git checkout -b pre-rebase D
```

### Durée de rétention dans le Reflog
Les commits originaux resteront disponibles dans le Reflog tant que :
- Tu n'as pas manuellement purgé le Reflog avec git reflog expire
- Git n'a pas effectué de garbage collection (par défaut, les objets non référencés sont supprimés après 90 jours)

## Conclusion
Les commits originaux D et E peuvent être retrouvés dans le Reflog, car Git conserve une trace des changements. Tant que le Reflog n'est pas purgé, tu peux inspecter, restaurer ou même recréer une branche à partir des commits originaux.







