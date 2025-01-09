# TP3 - Correction

## Structure finale du repository

```
repo/
├── alice/
│   └── presentation.md
├── bob/
│   └── presentation.md
└── charlie/
    └── presentation.md
```

## Exemple de contenu d'un fichier presentation.md

```markdown:alice/presentation.md
# Présentation

Nom : Dupont
Prénom : Alice
Date : 15/03/2024

## Personnalité admirée : Marie Curie

Marie Curie est une physicienne et chimiste polonaise naturalisée française.
Pionnière dans l'étude de la radioactivité, elle est la première femme à avoir
reçu un prix Nobel et la seule à en avoir reçu deux dans des domaines
scientifiques différents.
```

## Historique Git attendu

```
* 6ab8d23 (main) Merge pull request #3 from user/feat/charlie
|\
| * 2d4c789 feat: ajout description personnalité
| * 9f45e12 feat: ajout informations personnelles
| * 1a2b3c4 feat: création fichier présentation
|/
* 7890def Merge pull request #2 from user/feat/bob
|\
| * 3456789 feat: ajout description personnalité
| * bcdef01 feat: ajout informations personnelles
| * 2345678 feat: création fichier présentation
|/
* abcdef0 Merge pull request #1 from user/feat/alice
|\
| * 4567890 feat: ajout description personnalité
| * cdef012 feat: ajout informations personnelles
| * 3456789 feat: création fichier présentation
|/
* 1234567 Initial commit
```

## Points de validation

✅ Chaque personne a :

- Créé sa branche avec le bon nommage (feat/prenom)
- Créé son dossier et son fichier presentation.md
- Fait au moins 3 commits (création, informations, description)
- Créé une Pull Request
- Reviewé une Pull Request d'un collègue
- Mergé sa Pull Request dans main

> 💡 L'historique montre bien les branches temporaires qui ont été créées puis mergées via des Pull Requests.
