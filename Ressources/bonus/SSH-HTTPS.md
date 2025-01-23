# Gestion des connexions Git : SSH et HTTPS

## Passer de SSH à HTTPS

## Pourquoi passer de SSH à HTTPS ?
- Le port SSH (22) peut être bloqué par certains pare-feux d'entreprise
- HTTPS utilise le port 443 qui est généralement autorisé
- Configuration plus simple pour les débutants
- Authentification possible via token d'accès personnel

## Vérifier et modifier la configuration du dépôt
### Vérifier l'URL actuelle
```bash
git remote -v
```
Si vous voyez une URL de type SSH :
```bash
origin  git@github.com:username/repository.git (fetch)
origin  git@github.com:username/repository.git (push)
```

### Passer à HTTPS
```bash
git remote set-url origin https://github.com/username/repository.git
```

### Vérifier le changement
```bash
origin  https://github.com/username/repository.git (fetch)
origin  https://github.com/username/repository.git (push)
```

## Configuration de l'authentification HTTPS

### Méthode recommandée : Token d'accès personnel
1. Générer un token sur GitHub :
   - Aller dans Settings > Developer settings > Personal access tokens
   - Sélectionner "Tokens (classic)"
   - Générer un nouveau token avec les droits nécessaires (repo, workflow)
   - **Important** : Copier et sauvegarder le token, il ne sera plus visible après

2. Configurer Git pour utiliser le token :
```bash
git config --global credential.helper store
```

3. Lors du premier push, utiliser :
   - Username : votre nom d'utilisateur GitHub
   - Password : votre token d'accès personnel

### Configuration du cache des identifiants
Pour éviter de saisir les identifiants à chaque fois :
```bash
# Windows
git config --global credential.helper wincred

# macOS
git config --global credential.helper osxkeychain

# Linux
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'  # Cache pendant 1 heure
```

## Résolution des problèmes de connexion
### Problèmes avec le port SSH (22)
Si le port 22 est bloqué, plusieurs options s'offrent à vous :
1. Utiliser HTTPS (méthode recommandée en entreprise)
2. Configurer SSH sur un port alternatif (si autorisé) :
   ```bash
   # Dans ~/.ssh/config
   Host github.com
     Hostname ssh.github.com
     Port 443
   ```

### Tests de connectivité
Pour vérifier si le port SSH est accessible :
```bash
ssh -T -p 22 git@github.com
```
Cette commande permet de :
- `-T` : Désactiver l'allocation du terminal pseudo-TTY (utile car nous voulons juste tester la connexion, pas interagir avec un shell distant)
- `-p 22` : Spécifier explicitement le port 22 (port SSH par défaut)
- Tester la connexion SSH avec GitHub
- Si la connexion réussit, vous verrez un message du type : "Hi username! You've successfully authenticated..."

Pour tester la connexion HTTPS :
```bash
curl -v https://github.com
```
Cette commande permet de :
- `-v` : Afficher le mode verbeux (verbose) qui montre les détails de la connexion
- Vérifier si HTTPS est accessible
- Afficher les certificats SSL/TLS utilisés
- Montrer les codes de réponse HTTP
- Identifier les éventuels problèmes de proxy ou de pare-feu




