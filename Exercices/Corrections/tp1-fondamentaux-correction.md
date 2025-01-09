# Correction TP1 - Collection avec Git

Cette correction utilise l'exemple d'une collection de jeux vidéo, mais les commandes sont similaires pour une collection de musiques ou de films.

> 💡 Penser à montrer pendant la correction l'utilisation de source control dans VS Code

## Étape 1 : Initialisation

```bash
# Création du dossier
mkdir ma-collection-jeux
cd ma-collection-jeux

# Initialisation du dépôt Git
git init
```

## Étape 2 : Structuration

```bash
# Création des fichiers de catégories
touch console-nintendo.txt console-playstation.txt console-xbox.txt

# Ajout au staging
git add .

# Premier commit
git commit -m "Ajout des catégories de jeux vidéo"
```

## Étape 3 : Ajout des favoris

```bash
# Édition du fichier Nintendo
echo "1. The Legend of Zelda: Breath of the Wild
2. Super Mario Odyssey
3. Metroid Prime
4. Fire Emblem: Three Houses
5. Splatoon 3" > console-nintendo.txt

git add console-nintendo.txt
git commit -m "Ajout des jeux Nintendo préférés"

# Édition du fichier PlayStation
echo "1. The Last of Us
2. God of War
3. Horizon Zero Dawn
4. Spider-Man
5. Final Fantasy VII Remake" > console-playstation.txt

git add console-playstation.txt
git commit -m "Ajout des jeux PlayStation préférés"

# Édition du fichier Xbox
echo "1. Halo Infinite
2. Forza Horizon 5
3. Gears 5
4. Sea of Thieves
5. Fable" > console-xbox.txt

git add console-xbox.txt
git commit -m "Ajout des jeux Xbox préférés"
```

## Étape 4 : Ajout multiple

```bash
# Création du nouveau fichier
echo "1. Stardew Valley
2. Hollow Knight
3. Hades" > jeux-independants.txt

# Ajout de jeux dans un fichier existant
echo "6. Ghost of Tsushima
7. Demon's Souls" >> console-playstation.txt

# Staging et commit des modifications
git add jeux-independants.txt console-playstation.txt
// ou
git add .
git commit -m "Ajout des jeux indépendants et mise à jour des jeux PlayStation"
```

## Étape 5 : Correction d'erreur

```bash
# Ajout d'une erreur (un jeu Xbox dans la liste Nintendo)
echo "6. Halo Infinite" >> console-nintendo.txt
git add console-nintendo.txt
git commit -m "Ajout avec erreur"

# Recherche des hash des derniers commits
git log --oneline

# Vérification de l'erreur
git diff hash-du-commit-avec-erreur hash-du-commit-sans-erreur

# Correction de l'erreur
git restore --source hash-du-commit-sans-erreur console-nintendo.txt
// ou
git restore --source HEAD~1 console-nintendo.txt
// HEAD est le commit actuel. HEAD~1 est le commit précédent.
git add console-nintendo.txt
git commit -m "Correction de l'erreur : suppression du jeu Xbox"
```

## Étape 6 : Suppression de catégorie

```bash
# Suppression du fichier
git rm console-xbox.txt
git commit -m "Suppression de la catégorie Xbox"
```

## Étape 7 : Exploration de l'historique

```bash
# Affichage de l'historique complet
git log

# Affichage résumé
git log --oneline

# Affichage de l'historique avec des graphiques
git log --graph

# Comparaison entre deux commits (remplacer les hash par ceux de votre historique)
git diff hash-du-commit-avec-erreur hash-du-commit-sans-erreur
```

### Résultat final attendu

Votre historique devrait ressembler à ceci :

```bash
git log --oneline
abc123 (HEAD) Suppression de la catégorie Xbox
def456 Correction de l'erreur : suppression du jeu Xbox
ghi789 Ajout avec erreur
jkl012 Ajout des jeux indépendants et mise à jour des jeux PlayStation
mno345 Ajout des jeux Xbox préférés
pqr678 Ajout des jeux PlayStation préférés
stu901 Ajout des jeux Nintendo préférés
vwx234 Ajout des catégories de jeux vidéo
```

> 💡 **Git Graph** : Montrer l'extension Git Graph dans VS Code

### Structure finale du projet

```
ma-collection-jeux/
├── console-nintendo.txt
├── console-playstation.txt
└── jeux-independants.txt
```
