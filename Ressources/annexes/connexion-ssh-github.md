# Connecter un ordinateur à GitHub via SSH

## Introduction

Pour se connecter en SSH à GitHub, il faut créer une paire de clés SSH sur votre ordinateur :

- Une **clé privée** (par exemple `id_rsa`)
- Une **clé publique** (par exemple `id_rsa.pub`)

La clé publique doit être ajoutée à votre compte GitHub dans **Settings > SSH and GPG keys**.

Lien direct : [GitHub SSH Keys Settings](https://github.com/settings/keys)

---

## Chemin des clés SSH par défaut

Sur macOS et Linux, les clés sont généralement générées et stockées dans le dossier `~/.ssh/` :

- Clé privée : `~/.ssh/id_rsa`
- Clé publique : `~/.ssh/id_rsa.pub`

`~` représente le dossier personnel de l’utilisateur.

---

## Générer une paire de clés SSH

Pour générer une paire de clés SSH, utilisez la commande suivante :

```bash
ssh-keygen -t rsa -b 4096 -C "email@example.com" -f ~/.ssh/id_rsa -N ""
```

### Explication des paramètres :

- **-t** : Type de clé (rsa, ecdsa, ed25519)
- **-b** : Taille de la clé (4096 bits pour une sécurité élevée)
- **-C** : Commentaire (utilisez l’email associé à votre compte GitHub)
- **-f** : Chemin où la clé privée sera sauvegardée
- **-N** : Passphrase (laissez vide pour ne pas en avoir)

### Pourquoi utiliser l’email comme commentaire ?

Cela permet d’identifier facilement la clé dans votre compte GitHub, bien que vous puissiez utiliser n’importe quel texte.

---

## Ajouter la clé SSH à l’agent SSH

Une fois la clé générée, vous devez l’ajouter à l’agent SSH :

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

### Qu’est-ce que l’agent SSH ?

L’agent SSH est un programme qui garde en mémoire les clés privées actives pour éviter d’avoir à les retaper à chaque utilisation.

### Pourquoi cette étape est-elle nécessaire ?

Cela permet à Git et d’autres outils SSH de trouver automatiquement votre clé privée lorsqu’ils en ont besoin.

### `eval` est-il disponible sur tous les systèmes ?

Oui, `eval` fonctionne sur Linux, macOS et Windows (via Git Bash).

---

## Ajouter la clé publique dans GitHub

1. Copiez le contenu de votre clé publique :

   ```bash
   cat ~/.ssh/id_rsa.pub
   ```

2. Collez-la dans **Settings > SSH and GPG keys > New SSH key** dans votre compte GitHub.
3. Donnez un titre à votre clé (par exemple "macbook-pro-de-jean").

Lien direct : [GitHub SSH Keys Settings](https://github.com/settings/keys)

---

## Tester la connexion SSH

Testez la connexion SSH avec la commande suivante :

```bash
ssh -T git@github.com
```

Si tout est configuré correctement, vous verrez un message comme :

```bash
Hi jean-moulin! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## Particularité pour Windows

Le plus simple est d’installer **Git Bash**, qui inclut `ssh-keygen` et est prêt à l’emploi.
