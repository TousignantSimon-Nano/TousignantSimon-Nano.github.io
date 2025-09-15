# Théorie : Le fichier .bashrc en Linux

## 1. Qu’est-ce que `.bashrc` ?
- `.bashrc` est un fichier de **configuration spécifique à chaque utilisateur**.
- Il est exécuté à chaque ouverture d’un terminal interactif (bash).
- Il permet de **personnaliser l’environnement** du shell : variables, alias, fonctions, PATH, etc.

---

## 2. Localisation
Le fichier `.bashrc` se trouve dans le **répertoire personnel** de l’utilisateur :
```bash
/home/utilisateur/.bashrc

```bash
nano ~/.bashrc
```

## 3. Utilisations courantes

### 1. Ajouter des répertoires à PATH :
```bash
export PATH=$PATH:/home/utilisateur/mes_scripts
```

### 2. Définir des alias :

```bash
alias ll='ls -la'
```

### 3. Définir des variables d’environnement :
```bash
export EDITOR=nano
```

## 4. Appliquer les modifications

Après avoir modifié .bashrc, il faut recharger le fichier pour appliquer les changements sans fermer le terminal :
```bash
source ~/.bashrc
```

## 5. Bonnes pratiques

Toujours faire une sauvegarde avant de modifier .bashrc
```bash
cp ~/.bashrc ~/.bashrc.backup
```

Éviter de supprimer les configurations existantes si vous ne savez pas à quoi elles servent.

Utiliser .bashrc pour tout ce qui doit s’appliquer à chaque session interactive.
