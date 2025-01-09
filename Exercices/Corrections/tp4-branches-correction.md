# TP4 - Correction

## Structure finale du repository

```
repo/
├── alice/
│   └── presentation.md
├── bob/
│   └── presentation.md
└── team-charter.md
```

## Exemple de contenu d'un fichier presentation.md après modifications

```markdown:alice/presentation.md
# Présentation

Nom : Dupont
Prénom : Alice
Date : 15/03/2024

## Compétences techniques
- Languages : JavaScript, Python, SQL
- Frameworks : React, Express, Django
- Outils : VS Code, Git, Docker

## Soft Skills
- Travail d'équipe
- Communication
- Gestion du temps

## Centres d'intérêt
- Développement web
- Intelligence artificielle
- DevOps

// Suggestion de Bob : ajouter Docker aux compétences
```

## Exemple de team-charter.md après résolution

```markdown:team-charter.md
# Charte d'équipe

## Nos Valeurs
- Respect
- Collaboration
- Innovation

## Nos Objectifs
- Livrer des features de qualité
- Maintenir un code propre
- Partager les connaissances
- Améliorer la couverture de tests
- Réduire la dette technique
- Former les nouveaux membres

## Nos Méthodes
- Daily stand-up
- Code review
- Documentation
```

## Historique Git attendu

```
* 9ab8c23 (main) Merge branch 'feature/charter-bob'
|\
| * 5d4e789 feat: mise à jour objectifs équipe
* | 1f45g12 Merge branch 'feature/charter-alice'
|\|
| * 8a2b3c4 feat: ajout nouveaux objectifs
|/
* 7890def Merge branch 'feature/review-bob'
|\
| * 3456789 feat: suggestions pour Alice
| * bcdef01 feat: mise à jour compétences
|/
* abcdef0 Merge branch 'feature/review-alice'
|\
| * 4567890 feat: suggestions pour Bob
| * cdef012 feat: mise à jour compétences
|/
* 1234567 Merge branch 'feature/profile-bob'
|\
| * 3456789 feat: ajout sections profil Bob
|/
* abcd123 Merge branch 'feature/profile-alice'
|\
| * 4567890 feat: ajout sections profil Alice
|/
```

## Points de validation

✅ Exercice 1 - Chaque personne a :

- Créé et mergé sa branche feature/profile
- Créé sa branche feature/review
- Modifié son profil et celui de son binôme
- Résolu les conflits lors du merge

✅ Exercice 2 :

- Création du fichier team-charter.md
- Modifications simultanées des objectifs
- Résolution du conflit
- Historique final cohérent

> 💡 L'historique montre bien les différentes phases de l'exercice et la gestion des conflits via les merges.
