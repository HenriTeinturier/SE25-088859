# Commandes de Base du Terminal Bash

## Navigation dans les Dossiers

- `pwd` : Affiche le chemin du dossier courant (_Print Working Directory_)
- `cd` : Changer de dossier (_Change Directory_)
  - `cd ..` : Remonter au dossier parent
  - `cd ~` : Aller au répertoire personnel (home)
  - `cd /chemin/vers/dossier` : Aller vers un dossier spécifique

## Gestion des Fichiers et Dossiers

### Lister et Afficher

- `ls` : Lister les fichiers
  - `ls -a` : Lister tous les fichiers (y compris les cachés)
  - `ll` ou `ls -l` : Lister avec détails (permissions, taille, date...)
- `cat fichier.txt` : Afficher le contenu d'un fichier

### Création et Suppression

- `touch fichier.txt` : Créer un fichier vide
- `mkdir dossier` : Créer un dossier
- `rm fichier.txt` : Supprimer un fichier
- `rmdir dossier` : Supprimer un dossier vide
- `rm -r dossier` : Supprimer un dossier et son contenu

⚠️ **ATTENTION** : La commande `rm` supprime définitivement les fichiers (pas de corbeille)

### Manipulation de Texte

- `echo "texte"` : Afficher du texte dans le terminal
- `echo "texte" > fichier.txt` : Écrire dans un fichier (écrase le contenu)
- `echo "texte" >> fichier.txt` : Ajouter à la fin d'un fichier

### nano

nano est un éditeur de texte simple et puissant.

- `nano fichier.txt` : Editer un fichier avec nano
- `ctrl + o` : Sauvegarder le fichier
- `ctrl + x` : Quitter nano

## Permissions et Utilisateurs

- `whoami` : Afficher l'utilisateur courant
- `sudo commande` : Exécuter une commande en tant qu'administrateur (Linux/Mac)
- `su - utilisateur` : Changer d'utilisateur (Linux)

### Comprendre les Permissions (format `-rw-r--r--`)

Position Signification
1 Type (- pour fichier, d pour dossier)
2-4 Permissions du propriétaire (rwx)
5-7 Permissions du groupe (rwx)
8-10 Permissions des autres (rwx)
r : read (lecture)
w : write (écriture)
x : execute (exécution)

Exemple de lecture des permissions :

```
drwxr-xr-x 2 alice users  4096 Jan 15 14:30 Documents/
-rw-r--r-- 1 alice users   217 Jan 15 14:32 notes.txt
│└┬─┘└┬┘└┬┘ │ │     │      │    │           └── Nom du fichier
│ │   │  │  │ │     │      │    └── Date de modification
│ │   │  │  │ │     │      └── Taille
│ │   │  │  │ │     └── Groupe
│ │   │  │  │ └── Propriétaire
│ │   │  │  └── Nombre de liens
│ │   │  └── Permissions autres (r-x ou r--)
│ │   └── Permissions groupe (r-x ou r--)
│ └── Permissions propriétaire (rwx ou rw-)
└── Type (d=dossier, -=fichier)
```

## Autres Commandes Utiles

- `clear` : Nettoyer l'affichage du terminal
