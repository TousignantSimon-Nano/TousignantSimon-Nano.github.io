# Connexion à un dossier distant via SSH dans l’explorateur de fichiers

## 1. Introduction

Il est possible d’accéder à un répertoire distant via le protocole **SSH** directement depuis l’explorateur de fichiers de votre système d’exploitation.  
Cette méthode est pratique pour transférer, modifier ou consulter des fichiers sur un serveur (ou un Raspberry Pi) sans utiliser la ligne de commande.

---

## 2. Principe général

L’accès se fait via une **URI SSH** au format :

```
ssh://utilisateur@adresse_ip[:port]/chemin/dossier
```

### Exemple concret

```
ssh://robert@192.168.1.25/home/robert/
```

Ce lien permet de monter le dossier `/home/robert/` du Raspberry Pi (adresse IP `192.168.1.25`) dans votre explorateur de fichiers, en utilisant l’utilisateur `robert`.

---

## 3. Utilisation selon le système d’exploitation

### 3.1. Sous Linux (GNOME, Nautilus, Thunar, etc.)

1. Ouvrez votre explorateur de fichiers.  
2. Appuyez sur **Ctrl + L** pour accéder à la barre d’adresse.  
3. Entrez l’URI suivante :  
   ```
   ssh://robert@192.168.1.25/home/robert/
   ```
4. Une fenêtre d’authentification s’ouvrira — entrez le mot de passe de `robert`.  
5. Le dossier distant sera monté et accessible comme un dossier local.  

**Chemin monté :**
```
/run/user/<UID>/gvfs/sftp:host=192.168.1.25,user=robert/home/robert/
```

> 💡 Vous pouvez ensuite créer un **raccourci** ou un **signet** pour un accès rapide.

---

### 3.2. Sous macOS (Finder)

1. Dans Finder, ouvrez le menu **Aller → Se connecter au serveur...**  
   ou utilisez le raccourci **⌘ + K**.  
2. Entrez l’adresse du serveur :  
   ```
   ssh://robert@192.168.1.25/home/robert/
   ```
3. Cliquez sur **Connecter** et saisissez le mot de passe.  
4. Le dossier distant apparaîtra dans la barre latérale du Finder.

> 🍏 Sur macOS, le montage SSH utilise le protocole SFTP (inclus dans SSH).

---

### 3.3. Sous Windows (via WinSCP ou WSL)

#### Option 1 — Avec WinSCP
1. Téléchargez et installez **WinSCP** : [https://winscp.net](https://winscp.net)  
2. Créez une nouvelle session :  
   - **Protocole** : SFTP  
   - **Hôte** : `192.168.1.25`  
   - **Nom d’utilisateur** : `robert`  
   - **Mot de passe** : (celui de l’utilisateur `robert`)  
3. Cliquez sur **Enregistrer** puis **Connexion**.  
4. Le répertoire distant est alors accessible via une interface graphique semblable à l’explorateur.

#### Option 2 — Avec WSL (Windows Subsystem for Linux)
1. Ouvrez une fenêtre WSL (Ubuntu, Debian, etc.).  
2. Lancez le gestionnaire de fichiers de WSL :  
   ```bash
   nautilus ssh://robert@192.168.1.25/home/robert/
   ```
   > Si `nautilus` n’est pas installé, utilisez `xdg-open`.

---

## 4. Astuces avancées

- **Signets persistants** : la plupart des gestionnaires (Nautilus, Finder) permettent de sauvegarder les connexions SSH dans les favoris.  
- **Authentification par clé SSH** : si vous avez une clé publique installée dans `~/.ssh/authorized_keys` sur le Raspberry Pi, vous n’aurez plus besoin de saisir le mot de passe à chaque connexion.  
- **Ports personnalisés** : si votre serveur SSH utilise un port différent (ex. `2222`), ajoutez-le dans l’URI :  
  ```
  ssh://robert@192.168.1.25:2222/home/robert/
  ```

---

## 5. Dépannage

| Problème | Cause probable | Solution |
|-----------|----------------|-----------|
| Impossible de se connecter | SSH inactif sur le Raspberry Pi | Activez-le avec `sudo raspi-config` |
| Erreur « Connection refused » | Mauvais port SSH | Vérifiez la configuration dans `/etc/ssh/sshd_config` |
| Lenteur de transfert | Compression désactivée | Activez-la via la configuration SFTP |
| Dossier vide | Mauvais chemin distant | Vérifiez le chemin complet `/home/robert/` |

---

## 6. Références

- Documentation GNOME GVFS : [https://developer.gnome.org/gvfs/](https://developer.gnome.org/gvfs/)  
- Documentation OpenSSH : [https://www.openssh.com/](https://www.openssh.com/)  
- WinSCP : [https://winscp.net](https://winscp.net)  
