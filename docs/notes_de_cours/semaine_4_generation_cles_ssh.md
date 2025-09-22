# Guide pour étudiants : Ajouter une clé SSH avec PuTTY / KiTTY

Ce guide explique étape par étape comment générer une clé SSH sur Windows avec PuTTYgen et l’installer sur un serveur Linux.

---

## 1️⃣ Génération de la clé sur Windows (PuTTY / KiTTY)

1. Ouvrir **PuTTYgen** (dans le dossier d'instalation de putty / kitty ).  
2. Choisir **Type of key** : `RSA` et **4096 bits`.  
3. Cliquer sur **Generate** et bouger la souris pour créer de l’entropie.  
4. Mettre une **passphrase** pour sécuriser la clé (fortement recommandé).  
5. Exporter les fichiers :
   - **Private key** → `utilisateur.private.ppk` (clé privée, **à ne jamais partager**)  
   - **Public key** → `utilisateur.pub` (clé publique, utilisée sur le serveur)  
6. Copier la clé publique depuis la zone **“Public key for pasting into OpenSSH authorized_keys file”**.  
   - Cette version est **une seule ligne**, prête à être collée dans `authorized_keys`.

---

## 2️⃣ Installer la clé publique sur le serveur Linux

1. Se connecter au serveur avec un compte ayant les droits.  
2. Aller dans le **home** de l’utilisateur cible et créer le dossier `.ssh` si nécessaire :
```bash
mkdir -p /home/utilisateur/.ssh
chmod 700 /home/utilisateur/.ssh
```

3. Créer ou éditer le fichier `authorized_keys` :
```bash
nano /home/utilisateur/.ssh/authorized_keys
```

4. Coller la **ligne copiée depuis PuTTYgen** (clé publique OpenSSH).  
5. Sauvegarder et quitter l’éditeur.

6. Définir les bonnes permissions :
```bash
chmod 600 /home/utilisateur/.ssh/authorized_keys
chown -R utilisateur:utilisateur /home/utilisateur/.ssh
```

---

## 3️⃣ Connexion avec PuTTY / KiTTY

1. Ouvrir **PuTTY / KiTTY** → Session → entrer l’adresse du serveur.  
2. Aller dans **Connection → SSH → Auth** → **Private key file for authentication** → sélectionner `utilisateur.private.ppk`.  
3. Cliquer sur **Open** pour se connecter.  
   - Si une passphrase a été mise, la saisir.  

---

## ✅ Bonnes pratiques de sécurité

- La **clé privée ne doit jamais être partagée**.  
- La clé publique peut être copiée sur plusieurs serveurs.  
- Mettre toujours une **passphrase** pour la clé privée.  
- Vérifier les permissions de `~/.ssh` et `authorized_keys` sur le serveur.  
- Supprimer toute clé privée de supports externes après usage sécurisé.

---
