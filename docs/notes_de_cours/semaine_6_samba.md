# Samba et interopérabilité avec Windows

# Samba et interopérabilité avec Windows

**Samba** est une implémentation libre du protocole **SMB/CIFS** (Server Message Block / Common Internet File System), utilisé par Microsoft Windows pour le partage de fichiers, d’imprimantes et de ressources réseau.

## Fonctionnalités principales

- Partage de dossiers et imprimantes entre Linux/Unix et Windows  
- Intégration dans un domaine Windows **Active Directory**  
- Authentification via les comptes Windows  
- Possibilité pour un serveur Linux de fonctionner comme un serveur de fichiers Windows  

## Avantages

- Permet une interopérabilité fluide entre Linux et Windows  
- Facilite le déploiement de solutions mixtes dans un environnement réseau existant  
- Maintient la compatibilité avec les outils Windows standard

---

## Schéma simplifié

```text
+----------------+        +----------------+        +----------------+
|                |  SMB   |                |  SMB   |                |
|   Linux/Unix   +-------->     Samba      +-------->    Windows     |
|   (serveur)    |        |   (serveur)    |        |  (client)     |
+----------------+        +----------------+        +----------------+

---

## Exemple simple de partage Samba

1. Installer Samba :  
```bash
sudo apt install samba   # Debian/Ubuntu
sudo yum install samba   # CentOS/RHEL
```
2. Configurer un partage dans /etc/samba/smb.conf :  
```ini
[partage]
   path = /srv/partage
   read only = no
   browsable = yes
```
3. Redémarrer le service :
```bash 
sudo systemctl restart smbd
```

4. Accéder via windows 
-> explorateur -> chemin d'accès -> \\nom_serveur\partage


## Problèmes courants avec Samba et Windows

1. Chiffrement et compatibilité :
Windows utilise souvent le chiffrement SMB3 pour les partages récents. Si le serveur Samba est ancien ou mal configuré, Windows peut refuser la connexion. Les erreurs typiques incluent “Access denied” ou “Connection refused”. Cela peut aussi provoquer des problèmes d’authentification avec Active Directory.

Solutions :

Mettre Samba à jour vers une version récente (4.10+ recommandée).

Configurer le protocole SMB et le chiffrement dans smb.conf pour exiger SMB3 et le chiffrement.

Vérifier que le client Windows accepte le protocole utilisé (SMB2/SMB3).

2. Problèmes de permissions :
Les droits Samba ne sont pas toujours identiques aux permissions Linux/Unix. Vérifier les permissions POSIX et la directive valid users dans smb.conf.

3. Problèmes d’utilisateur ou mot de passe :
Si Windows ne reconnaît pas un utilisateur, vérifier la synchronisation des comptes Samba/AD. On peut utiliser pdbedit -L pour lister les utilisateurs Samba.

4. Partages non visibles :
Si le partage n’apparaît pas dans l’explorateur Windows, vérifier que browsable = yes est activé, et que le firewall Linux laisse passer le port TCP 445.

5. Encodage des caractères :
Les noms de fichiers avec accents ou caractères spéciaux peuvent poser problème. On peut ajouter dans smb.conf :
``` ini
unix charset = UTF-8

display charset = UTF-8
```