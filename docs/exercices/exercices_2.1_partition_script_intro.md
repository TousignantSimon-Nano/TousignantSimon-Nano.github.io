# Exercices Raspberry Pi – Gestion des partitions et montages

## Contexte
- Raspberry Pi avec Raspbian OS installé sur **clé USB**.  
- Carte SD utilisée pour stocker deux partitions :  
  - 1 partition **NTFS**  
  - 1 partition **EXT4**  

---

## Exercice 1 – Partitionnement et formatage
1. Créer une partition au format **EXT4** sur la carte SD.  
2. Créer une partition au format **NTFS** sur la carte SD.  

---

## Exercice 2 – Montage automatique (EXT4)
- Monter automatiquement la partition EXT4 sur le dossier :  
  ```
  /var/www/site_principal
  ```
- Le dossier doit être créé s’il n’existe pas.  
- Le montage doit être défini dans le fichier `/etc/fstab`.  

---

## Exercice 3 – Montage manuel (NTFS)
- Monter manuellement la partition NTFS sur :  
  ```
  /home/utilisateur/dossier personnel
  ```
- Le démontage doit aussi se faire manuellement.  

---

## Exercice 4 – Scripts
1. Créer un script `mount_perso.sh` dans `/home/utilisateur/` qui monte la partition NTFS.  
2. Créer un script `unmount_perso.sh` dans `/home/utilisateur/` qui démonte la partition NTFS.  
3. Créer un script `menu_perso.sh` dans `/home/utilisateur/` qui propose un menu avec deux choix :  
   - (1) Monter `/home/utilisateur/dossier personnel`  
   - (2) Démonter `/home/utilisateur/dossier personnel`  

---

## Glossaire des commandes autorisées

### Partitionnement
- `parted` : gestion des partitions  
- `fdisk` : partitionnement en mode texte  
- `gparted` : outil graphique pour partitions  

### Formatage
- `mkfs.ext4` : formatage en EXT4  
- `mkfs.ntfs` : formatage en NTFS  

### Identification des partitions et UUID
- `lsblk` : lister les disques et partitions  
- `blkid` : afficher les UUID et types de systèmes de fichiers  

### Montage / Démontage
- `mount` : monter une partition  
- `umount` : démonter une partition  
- `/etc/fstab` : configuration du montage automatique  

### Gestion des répertoires
- `mkdir` : création de dossiers  

### Scripts
- `nano`, `vim` : éditeurs de scripts  
- `bash` : exécution de scripts  
- `chmod +x` : rendre un script exécutable  

### Structures de script
- `case` : exécution conditionnelle avec choix  
- `select` : création de menus interactifs  

---
