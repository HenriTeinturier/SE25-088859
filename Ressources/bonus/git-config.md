# Configuration Git approfondie

## Comprendre les niveaux de configuration

Git utilise un système de configuration hiérarchique avec trois niveaux, fonctionnant comme des "couches" qui se superposent. Chaque niveau peut écraser les configurations des niveaux précédents.

### 1. Niveau Système (`--system`)
- **Emplacement** : `/etc/gitconfig` (Linux/Mac) ou `C:\Program Files\Git\etc\gitconfig` (Windows)
- **Portée** : Affecte TOUS les utilisateurs et TOUS les dépôts de la machine
- **Permissions** : Nécessite des droits administrateur pour modifier
- **Cas d'usage** : 
  - Configuration de proxy d'entreprise
  - Politiques de sécurité communes
  - Standards d'équipe

```bash
# Exemple : Configurer un proxy d'entreprise pour tous les utilisateurs
sudo git config --system http.proxy http://proxy.entreprise.com:8080

# Lister les configurations système
git config --system --list

# Emplacement du fichier
echo "Fichier système : $(git config --system --show-origin core.editor)"
```

### 2. Niveau Global (`--global`)
- **Emplacement** : 
  - Linux/Mac : `~/.gitconfig` ou `~/.config/git/config`
  - Windows : `C:\Users\<USER>\.gitconfig`
- **Portée** : Spécifique à votre utilisateur, affecte TOUS vos dépôts
- **Permissions** : Modifiable par l'utilisateur courant
- **Cas d'usage** :
  - Identité personnelle (nom, email)
  - Préférences d'éditeur
  - Alias personnels
  - Configuration SSH/HTTPS

```bash
# Configurations courantes au niveau global
git config --global user.name "Votre Nom"
git config --global user.email "vous@example.com"

# Voir le contenu du fichier global
cat ~/.gitconfig  # Linux/Mac
type %USERPROFILE%\.gitconfig  # Windows

# Vérifier l'emplacement exact du fichier global
git config --global --list --show-origin
```

### 3. Niveau Local (par défaut)
- **Emplacement** : `.git/config` dans le dépôt
- **Portée** : Uniquement le dépôt courant
- **Priorité** : Écrase les configurations système et globales
- **Cas d'usage** :
  - Email professionnel différent pour un projet
  - Configurations spécifiques au projet
  - Hooks particuliers

```bash
# Exemple : Configuration spécifique à un projet
git config user.email "projet@entreprise.com"

# Voir les configurations locales
git config --local --list

# Éditer directement le fichier de config local
git config --edit
```

### Ordre de priorité et héritage
1. Git cherche d'abord dans le niveau **Local** (`.git/config`)
2. Si non trouvé, cherche dans le niveau **Global** (`~/.gitconfig`)
3. Si toujours non trouvé, utilise le niveau **Système** (`/etc/gitconfig`)

```bash
# Voir toutes les configurations avec leur origine
git config --list --show-origin

# Voir la valeur effective d'une configuration
git config user.email  # Montre la valeur qui sera réellement utilisée

# Voir les configurations avec leur niveau (scope)
git config --list --show-scope
```

### Test et vérification
```bash
# Tester si une configuration existe
git config --get user.name || echo "Non configuré"

# Voir d'où vient une configuration spécifique
git config --show-origin user.email

# Lister toutes les configurations avec leur niveau
git config --list --show-scope
```

## Localisation et édition des fichiers de configuration

### Afficher les configurations
```bash
# Afficher toutes les configurations et leur origine
git config --list --show-origin

# Afficher une configuration spécifique
git config user.name

# Afficher les configurations avec leur scope
git config --list --show-scope
```

### Édition directe des fichiers
```bash
# Éditer la configuration globale
git config --global --edit

# Éditer la configuration locale
git config --edit
```

## Configurations essentielles

### Identité et authentification
L'identité Git est utilisée pour signer vos commits et est visible dans l'historique.
```bash
# Identité de base pour vos commits
git config --global user.name "Nom Prénom"
git config --global user.email "email@domaine.com"

# Stockage des credentials (identifiants)
git config --global credential.helper cache  # Stockage temporaire en mémoire
git config --global credential.helper 'cache --timeout=3600'  # Cache pendant 1h
```
Les "credentials" sont vos identifiants (username/password ou token) pour les dépôts distants. Le credential helper évite de les retaper à chaque opération (push, pull, etc.).

### Performance et optimisation
```bash
# Parallélisme : accélère les opérations Git sur les CPU multi-cœurs
git config --global core.parallel true  # Utile pour les gros dépôts
git config --global pack.threads "0"    # "0" = utilise tous les cœurs disponibles

# Compression : optimise la taille du dépôt
git config --global core.compression 9    # Niveau max de compression
git config --global pack.compression 9    # Pour les objets packés

# Cache en mémoire : accélère les opérations Git
git config --global core.preloadindex true  # Charge l'index en mémoire
git config --global core.fscache true       # Cache les stats des fichiers
```
- Le parallélisme est particulièrement utile pour les gros dépôts ou les opérations lourdes (clone, gc)
- La compression réduit l'espace disque mais augmente légèrement le temps CPU
- Les caches mémoire améliorent les performances, surtout sur Windows et les gros projets

### Merge et Diff
```bash
# Configuration des outils de merge
git config --global merge.tool vimdiff              # Outil pour résoudre les conflits
git config --global mergetool.prompt false         # Évite les prompts à chaque fichier

# Configuration des outils de diff
git config --global diff.tool vscode               # VS Code pour voir les différences
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'

# Stratégie de merge
git config --global merge.ff false        # Force un commit de merge explicite
git config --global pull.rebase true      # Préfère rebase à merge lors des pulls
```
Ces configurations définissent comment Git gère les différences et les fusions de code.

### Formatage et encodage
```bash
# Gestion des fins de ligne (crucial pour les équipes cross-platform)
git config --global core.autocrlf input   # Pour Linux/Mac
git config --global core.autocrlf true    # Pour Windows

# Encodage pour support multilingue
git config --global core.quotepath false     # Affiche correctement les caractères UTF-8
git config --global i18n.commitEncoding utf-8
git config --global i18n.logOutputEncoding utf-8
```
- `autocrlf` gère la conversion des fins de ligne entre Windows (CRLF) et Unix (LF)
- Les configurations d'encodage sont essentielles pour les projets internationaux ou avec caractères spéciaux

### Alias puissants
Les alias sont des raccourcis personnalisés pour les commandes fréquentes :
```bash
# Log graphique amélioré
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# Raccourcis pratiques
git config --global alias.cob "checkout -b"  # Création et switch de branche
git config --global alias.st "status -sb"    # Status concis
git config --global alias.cm "commit -m"     # Commit avec message
```

### Hooks globaux
Les hooks sont des scripts exécutés automatiquement à certains moments (pre-commit, pre-push, etc.) :
```bash
# Définir un dossier global pour les hooks
git config --global core.hooksPath ~/.git-hooks
```
Exemple d'utilisation : validation de code, tests automatiques, formatage avant commit.

### Sécurité
```bash
# Vérification SSL pour les connexions HTTPS
git config --global http.sslVerify true    # Protège contre les attaques MITM

# Signature des commits avec GPG
git config --global commit.gpgsign true              # Signe tous les commits
git config --global user.signingkey <YOUR-GPG-KEY-ID>  # Clé GPG à utiliser
```
- La vérification SSL assure des connexions sécurisées
- La signature GPG prouve l'authenticité de vos commits (important pour les projets sensibles)

## Configurations avancées

### Alias puissants
```bash
# Log amélioré
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# Checkout avec création de branche
git config --global alias.cob "checkout -b"

# Status court
git config --global alias.st "status -sb"

# Commit avec message
git config --global alias.cm "commit -m"
```

### Hooks globaux
```bash
# Définir un répertoire de hooks global
git config --global core.hooksPath ~/.git-hooks
```

### Sécurité
```bash
# Vérifier les certificats SSL
git config --global http.sslVerify true

# Signer automatiquement les commits
git config --global commit.gpgsign true
git config --global user.signingkey <YOUR-GPG-KEY-ID>
```

## Configuration par dépôt

### Surcharge des configurations globales
Pour configurer un dépôt spécifique, naviguez dans le dépôt et utilisez git config sans --global :
```bash
cd /chemin/vers/depot
git config user.email "projet.specifique@entreprise.com"
git config core.ignorecase false
```

### Configurations conditionnelles
Vous pouvez utiliser des configurations conditionnelles dans votre fichier .git/config :
```ini
[includeIf "gitdir:~/travail/"]
    path = ~/.gitconfig-travail
[includeIf "gitdir:~/perso/"]
    path = ~/.gitconfig-perso
```

## Bonnes pratiques

1. **Vérification régulière** : Auditez vos configurations périodiquement
   ```bash
   git config --list --show-origin | grep -v '^file:'
   ```

2. **Documentation** : Commentez vos configurations personnalisées
   ```bash
   # Dans .gitconfig
   # [alias]
   #   # Affiche un log coloré et formaté
   #   lg = log --color --graph --pretty=format:'%Cred%h%Creset ...'
   ```

3. **Sauvegarde** : Versionnez vos fichiers de configuration
   ```bash
   # Exemple de script de backup
   cp ~/.gitconfig ~/dotfiles/git/
   ```

## Dépannage

### Réinitialisation des configurations
```bash
# Supprimer une configuration spécifique
git config --unset user.email

# Supprimer une section entière
git config --remove-section core

# Réinitialiser toutes les configurations locales
rm .git/config && git config --local core.autocrlf input
```

### Débogage
```bash
# Tracer l'origine
