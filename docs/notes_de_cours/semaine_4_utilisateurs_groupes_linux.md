
# Gestion des utilisateurs et groupes sous Linux

## 1. Utilisateurs et groupes

Sous Linux, tout utilisateur appartient à un ou plusieurs **groupes**.  
- **Utilisateur** : une personne ou un service pouvant se connecter ou exécuter des tâches.  
- **Groupe** : un ensemble d'utilisateurs partageant des droits communs sur des fichiers ou dossiers.

### Vérifier l'utilisateur courant
```bash
whoami
```

### Vérifier les groupes d’un utilisateur
```bash
groups nom_utilisateur
```

## 2. Ajouter un utilisateur

La commande principale pour ajouter un utilisateur est `useradd`.  
Exemple simple :
```bash
sudo useradd nom_utilisateur
```

Pour créer l’utilisateur avec un répertoire personnel (`/home/nom_utilisateur`) :
```bash
sudo useradd -m nom_utilisateur
```

Pour spécifier un shell par défaut :
```bash
sudo useradd -m -s /bin/bash nom_utilisateur
```

### Ajouter un mot de passe à l’utilisateur
```bash
sudo passwd nom_utilisateur
```

## 3. Supprimer un utilisateur

Pour supprimer un utilisateur :
```bash
sudo userdel nom_utilisateur
```

Pour supprimer aussi son répertoire personnel :
```bash
sudo userdel -r nom_utilisateur
```

## 4. Modifier un utilisateur

### Changer le mot de passe
```bash
sudo passwd nom_utilisateur
```

### Modifier le shell
```bash
sudo usermod -s /bin/zsh nom_utilisateur
```

### Ajouter un utilisateur à un groupe
```bash
sudo usermod -aG nom_groupe nom_utilisateur
```
> **Attention** : `-a` = append (ajouter sans retirer l’utilisateur des autres groupes)

## 5. Gestion des groupes

### Créer un groupe
```bash
sudo groupadd nom_groupe
```

### Supprimer un groupe
```bash
sudo groupdel nom_groupe
```

### Vérifier tous les groupes
```bash
getent group
```

## 6. Informations utiles

- Tous les utilisateurs sont listés dans `/etc/passwd`  
```bash
cat /etc/passwd
```

- Tous les groupes sont listés dans `/etc/group`  
```bash
cat /etc/group
```

- Vérifier l’utilisateur courant et son ID
```bash
id
```

## 7. Exemples pratiques

1. Créer un utilisateur `alice` avec répertoire personnel et mot de passe :
```bash
sudo useradd -m alice
sudo passwd alice
```

2. Ajouter `alice` au groupe `sudo` :
```bash
sudo usermod -aG sudo alice
```

3. Supprimer l’utilisateur `bob` et son répertoire personnel :
```bash
sudo userdel -r bob
```
