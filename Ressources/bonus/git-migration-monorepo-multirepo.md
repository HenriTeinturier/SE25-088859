# Migration vers Git : Monorepo vs Multi-repos

## Gestion du code partagé

### Structure recommandée pour un monorepo

```	
monorepo/
├── shared/          # Bibliothèques partagées
│   ├── ui/         # Composants UI réutilisables
│   └── utils/      # Utilitaires communs
├── project1/
│   ├── src/
│   └── CODEOWNERS
├── project2/
│   ├── src/
│   └── CODEOWNERS
└── .github/        # Configuration GitHub
    └── CODEOWNERS  # Règles globales
```

### Structure alternative avec bibliothèques internes

```
monorepo/
├── libs/           # Bibliothèques internes
│   ├── core/      # Fonctionnalités core
│   └── common/    # Utilitaires communs
├── apps/          # Applications
│   ├── app1/
│   └── app2/
└── packages/      # Packages publiables
    └── shared/
```

## Gestion des permissions

### 1. CODEOWNERS
```
# Équipes par domaine
/backend/*          @backend-team
/frontend/*         @frontend-team
/shared/*           @core-team

# Configurations sensibles
*.config.js         @lead-devs
/security/*         @security-team
```

### 2. Branch Protection avec GitBucket/GitHub Enterprise

```
protection_rules:
  main:
    paths:
      - "backend/*"
      - "frontend/*"
      - "shared/*"
    required_reviews: 2
    required_teams:
      - senior-devs
```

### 3. Permissions par équipe
```
teams:
  backend:
    paths:
      - "backend/*"
    permissions: write
  
  frontend:
    paths:
      - "frontend/*"
    permissions: write
  
  shared-lib:
    paths:
      - "shared/*"
    permissions: 
      read: ["*"]
      write: ["shared/*/docs"]
```

## Avantages du monorepo avec permissions granulaires

1. **Gestion centralisée**
   - Un seul point de vérité
   - Versions cohérentes des dépendances
   - CI/CD unifié

2. **Contrôle d'accès fin**
   - Permissions par chemin (path-based)
   - Règles de review spécifiques
   - Protection des parties sensibles

3. **Partage de code facilité**
   - Pas de gestion de versions entre repos
   - Refactoring global possible
   - Tests d'intégration simplifiés

## Avantages du multi-repos

1. **Isolation naturelle**
   - Séparation claire des responsabilités
   - Permissions simples par repo
   - Déploiements indépendants

2. **Performance**
   - Clonage plus rapide
   - Historique Git plus léger
   - CI/CD optimisée

## Recommandations pour la migration

### Analyse préalable
1. Cartographier les dépendances entre projets
2. Identifier les équipes et leurs besoins d'accès
3. Évaluer le volume de code partagé

### Choix de l'approche
- **Monorepo** si :
  - Fort couplage entre projets
  - Besoin de partage de code fréquent
  - Équipes transverses nombreuses
  - Besoin de contrôle d'accès granulaire par path

- **Multi-repos** si :
  - Projets vraiment indépendants
  - Équipes distinctes
  - Besoins de sécurité stricts
  - Pas ou peu de code partagé

### Migration progressive
1. Commencer par un projet pilote
2. Mettre en place les règles d'accès
3. Former les équipes aux nouvelles pratiques
4. Valider l'approche avant généralisation

# Migration vers Git : Gestion des autorisations avec GitBucket

## Gestion des permissions dans GitBucket

### Niveaux d'autorisation disponibles

1. **Permissions de base**
   - No Access
   - Read
   - Write
   - Admin

2. **Permissions avancées**
   - Read Source
   - Read Wiki
   - Read Issues
   - Write Source
   - Write Wiki
   - Write Issues
   - Manage Source
   - Manage Wiki
   - Manage Issues

### Structure avec Monorepo

```
monorepo/
├── restricted/        # Accès limité (équipe sécurité)
├── internal/         # Accès équipes internes
├── public/          # Accès tous développeurs
└── .gitbucket/      # Configuration GitBucket
    └── SECURITY     # Règles de sécurité
```

### Configuration des permissions GitBucket

```
# Configuration des permissions par dossier
repository:
  paths:
    "restricted/*":
      teams:
        security-team: admin
        dev-team: no-access
    
    "internal/*":
      teams:
        internal-dev: write
        external-dev: read
    
    "public/*":
      teams:
        "*": write
```

### Protection des branches

```
branch_protection:
  main:
    paths:
      - "restricted/*"
      - "internal/*"
    required_reviews: 2
    required_status_checks: true
    teams:
      security-team:
        required_review: true
```

## Comparaison Monorepo vs Multi-repos pour les permissions

### Monorepo

#### Avantages
- Gestion centralisée des permissions
- Possibilité de permissions par dossier
- Vue globale des accès
- Audit de sécurité centralisé

#### Limitations
- Granularité limitée aux dossiers
- Tous les développeurs voient la structure
- Risque d'exposition accidentelle
- Performance git clone (tout le repo)

### Multi-repos

#### Avantages
- Isolation totale des projets sensibles
- Permissions simples par repo
- Clone rapide (uniquement le nécessaire)
- Risques limités par projet

#### Limitations
- Gestion complexe des permissions
- Multiplication des configurations
- Difficulté de partage de code
- Audit de sécurité dispersé

## Recommandations

### Pour un Monorepo
1. Utiliser les Protected Paths
2. Définir des CODEOWNERS précis
3. Mettre en place des hooks de pré-commit
4. Auditer régulièrement les permissions

### Pour Multi-repos
1. Grouper les repos par niveau de sécurité
2. Utiliser des templates de permissions
3. Centraliser la gestion des accès
4. Documenter les accès requis

## Migration depuis un système legacy

1. **Audit des accès actuels**
   - Cartographier les permissions existantes
   - Identifier les zones sensibles
   - Documenter les besoins d'accès

2. **Choix stratégique**
   - Monorepo si besoin de granularité par dossier
   - Multi-repos si isolation totale nécessaire

3. **Plan de migration**
   - Définir la nouvelle structure
   - Configurer les permissions GitBucket
   - Former les équipes aux nouvelles pratiques
