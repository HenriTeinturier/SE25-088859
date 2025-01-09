# États des fichiers dans Git

Dans Git, un fichier peut se trouver dans l'un des quatre états suivants :

## Untracked (Non suivi)

- Fichier présent dans le Working Directory
- Non suivi par Git
- N'a jamais été ajouté à l'index
- Ne provient pas d'un commit précédent

## Unmodified (Non modifié)

- Fichier suivi par Git
- Identique à la version du dernier commit
- Présent dans l'historique des commits
- Aucune modification détectée

## Modified (Modifié)

- Fichier suivi par Git
- Modifications détectées depuis le dernier commit
- Changements non encore indexés
- Nécessite `git add` pour passer en Staged

## Staged (Indexé)

- Fichier ajouté à la Staging Area
- Modifications prêtes pour le prochain commit
- Ajouté via la commande `git add`
- En attente d'être enregistré définitivement

## Cycle de vie des fichiers

![Cycle de vie des fichiers dans Git](../assets/suivi-fichiers.png)

Le schéma ci-dessus montre les transitions possibles entre les différents états :

- `Add the file` : Ajoute un fichier non suivi au suivi Git
- `Edit the file` : Modification d'un fichier suivi
- `Stage the file` : Indexation des modifications
- `Commit` : Enregistrement des modifications indexées
- `Remove the file` : Suppression du suivi du fichier

> 💡 **Note** : Un fichier peut passer d'un état à l'autre au fil de vos actions. Par exemple, après un commit, un fichier Staged redevient Unmodified.
