# Commande `scp` — Transfert sécurisé de fichiers

## 1. Introduction

La commande **`scp` (Secure Copy Protocol)** est un outil de transfert de fichiers sécurisé basé sur le protocole **SSH**.  
Elle permet de copier des fichiers entre un système local et un système distant, ou entre deux systèmes distants, tout en chiffrant les données transférées.

`scp` est particulièrement utile dans des environnements Linux/Unix et sur **Raspberry Pi**, où il facilite le transfert de fichiers sans configuration supplémentaire, tant que l’accès SSH est activé.

---

## 2. Syntaxe de base

```bash
scp [options] source destination
```

### Exemple général

- Copier un fichier **local vers distant** :
  ```bash
  scp fichier.txt robert@192.168.1.25:/home/robert/
  ```

- Copier un fichier **distant vers local** :
  ```bash
  scp robert@192.168.1.25:/home/robert/fichier.txt ./
  ```

- Copier un répertoire **entier** :
  ```bash
  scp -r dossier/ robert@192.168.1.25:/home/robert/
  ```

---

## 3. Options courantes

| Option | Description |
|:-------|:-------------|
| `-r` | Copie récursive (répertoires et sous-répertoires). |
| `-p` | Préserve les dates de modification, les modes et permissions du fichier. |
| `-P <port>` | Spécifie le port SSH à utiliser (par défaut : 22). |
| `-C` | Active la compression pour accélérer le transfert. |
| `-v` | Mode verbeux — affiche les détails du transfert et de la connexion. |
| `-q` | Mode silencieux — supprime les messages non essentiels. |
| `-l <limite>` | Limite la bande passante utilisée (en kilobits/s). |
| `-i <chemin_clef>` | Spécifie une clé privée pour l’authentification SSH. |

---

## 4. Exemples pratiques

### 4.1. Copier un fichier du poste local vers le Raspberry Pi
```bash
scp mon_script.py robert@192.168.1.25:/home/robert/
```

### 4.2. Copier un fichier du Raspberry Pi vers le poste local
```bash
scp robert@192.168.1.25:/home/robert/resultats.txt ./
```

### 4.3. Copier tout un répertoire
```bash
scp -r projet/ robert@192.168.1.25:/home/robert/projets/
```

### 4.4. Spécifier un port SSH différent
Si le serveur SSH écoute sur le port 2222 :
```bash
scp -P 2222 fichier.txt robert@192.168.1.25:/home/robert/
```

### 4.5. Transfert avec compression
```bash
scp -C image.iso robert@192.168.1.25:/home/robert/
```

---

## 5. Exercices pratiques

### Objectif pédagogique
Apprendre à utiliser la commande `scp` dans un contexte réseau avec **Raspberry Pi** et l’utilisateur **`robert`**.

### Pré-requis
- SSH activé sur le Raspberry Pi (`sudo raspi-config` → Interface Options → SSH → Enable)
- Adresse IP connue (ex. `192.168.1.25`)
- Compte utilisateur `robert` existant sur le Raspberry Pi

### Exercice 1 — Copier un script Python vers le Raspberry Pi
1. Sur votre machine locale, créez un fichier :
   ```bash
   echo "print('Hello Raspberry!')" > hello_pi.py
   ```
2. Copiez-le sur le Raspberry Pi :
   ```bash
   scp hello_pi.py robert@192.168.1.25:/home/robert/
   ```
3. Connectez-vous en SSH pour vérifier :
   ```bash
   ssh robert@192.168.1.25
   ls
   ```

### Exercice 2 — Récupérer un fichier généré sur le Raspberry Pi
1. Sur le Raspberry Pi, créez un fichier :
   ```bash
   echo "Log système du jour" > system_log.txt
   ```
2. Depuis votre machine locale :
   ```bash
   scp robert@192.168.1.25:/home/robert/system_log.txt ./
   ```

### Exercice 3 — Sauvegarde complète d’un répertoire
1. Créez un dossier `projets/` contenant plusieurs fichiers sur le Raspberry Pi.
2. Depuis votre machine locale, exécutez :
   ```bash
   scp -r robert@192.168.1.25:/home/robert/projets ./sauvegarde_pi/
   ```

### Exercice 4 — Utiliser un autre port SSH
1. Modifiez le port SSH du Raspberry Pi (par exemple 2222 dans `/etc/ssh/sshd_config`).
2. Redémarrez le service SSH :
   ```bash
   sudo systemctl restart ssh
   ```
3. Testez la commande :
   ```bash
   scp -P 2222 fichier.txt robert@192.168.1.25:/home/robert/
   ```

---

## 6. Bonnes pratiques & sécurité

- **Toujours utiliser des mots de passe forts** ou mieux, une **authentification par clé SSH**.
- Vérifiez les **permissions des fichiers transférés** (surtout en mode `-r`).
- Évitez de lancer `scp` en tant que `root` sauf nécessité absolue.
- En environnement pédagogique, configurez les ports et droits pour éviter les transferts non autorisés.
- Pour des transferts automatisés, préférez **`rsync -e ssh`** qui offre plus de contrôle et d’options d’optimisation.

---

## 7. Références

- `man scp`
- Documentation OpenSSH : [https://www.openssh.com/](https://www.openssh.com/)
- Tutoriel Raspberry Pi : [https://www.raspberrypi.com/documentation/computers/remote-access.html](https://www.raspberrypi.com/documentation/computers/remote-access.html)
