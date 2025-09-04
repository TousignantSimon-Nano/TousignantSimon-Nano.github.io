# Gestion des montages sur Raspberry Pi OS Bookworm (Debian 12)

---

## 1. Généralités
- Commandes principales : `mount`, `umount`
- Fichier de configuration automatique : `/etc/fstab`
- Les partitions peuvent être identifiées par **device** (`/dev/sda1`) ou par **UUID** (recommandé pour éviter les changements de nom).
- Points de montage recommandés :
  - **/mnt** : pour les montages temporaires ou administratifs, partitions internes ou systèmes.
  - **/media/user/** : pour les périphériques amovibles, détectés par l’environnement graphique.

---

## 2. Montage manuel

### a) Monter une partition
```bash
sudo mount /dev/sda1 /mnt/data
```
- `/dev/sda1` : périphérique ou partition
- `/mnt/data` : point de montage créé pour ce montage (préférable à `/media/user` pour les systèmes et partitions internes)

### b) Monter avec UUID
1. Trouver l’UUID :
```bash
blkid
```
Exemple :
```
/dev/sda1: UUID="123e4567-e89b-12d3-a456-426614174000" TYPE="ext4"
```
2. Monter via UUID :
```bash
sudo mount -U 123e4567-e89b-12d3-a456-426614174000 /mnt/data
```

### c) Options courantes
- `ro` : lecture seule
- `rw` : lecture/écriture
- `noexec` : ne pas exécuter de fichiers binaires
- `nosuid` : ignorer les SUID/SGID
- `hard` : pour les montages NFS, bloque les opérations jusqu’à ce que le serveur réponde
- `soft` : retourne une erreur en cas de timeout (NFS)

```bash
sudo mount -o rw,noexec /dev/sda1 /mnt/data
```

---

## 3. Démontage

### a) Démontage simple
```bash
sudo umount /mnt/data
```

### b) Démontage forcé et lazy
- **Lazy unmount (`-l`)** : détache le système de fichiers immédiatement, mais attend que tous les fichiers ouverts soient fermés avant de libérer complètement le montage.
```bash
sudo umount -l /mnt/data
```
- **Force unmount (`-f`)** : force le démontage même si le système de fichiers est occupé (utile pour NFS ou partitions corrompues).
```bash
sudo umount -f /mnt/data
```

> Note : `lazy` est plus sûr que `force` car il évite les risques de corruption.

---

## 4. Fichier `/etc/fstab`

Exemple avec UUID :
```
# <file system> <mount point> <type> <options> <dump> <pass>
UUID=123e4567-e89b-12d3-a456-426614174000 /mnt/data ext4 defaults 0 2
```

### a) Explication des colonnes
1. `file system` : périphérique ou UUID
2. `mount point` : répertoire de montage
3. `type` : ext4, vfat, ntfs, swap, etc.
4. `options` : defaults, ro, rw, noexec...
5. `dump` : 0 ou 1 (utilisé par dump)
6. `pass` : 0,1,2 (ordre pour fsck au boot)

---

## 5. Exemple complet

### a) Partition racine et /home
```
UUID=aaaa-bbbb / ext4 defaults 0 1
UUID=cccc-dddd /home ext4 defaults 0 2
```

### b) Partition swap (fichier ou partition)

#### Partition swap
```
UUID=eeee-ffff none swap sw 0 0
```

#### Fichier swap
```bash
sudo fallocate -l 1G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```
Ajouter dans `/etc/fstab` :
```
/swapfile none swap sw 0 0
```

---

## 6. Vérification

- Lister les montages actifs :
```bash
mount | column -t
```
- Vérifier le swap :
```bash
swapon --show
```

---

## 7. Notes pratiques

1. Toujours créer le point de montage (`mkdir /mnt/data`) avant `mount`.
2. Préférer UUID pour fiabilité.
3. Ne pas monter plusieurs fois la même partition.
4. Pour appliquer `/etc/fstab` sans reboot :
```bash
sudo mount -a
```
5. Préférer `lazy` pour démonter un système de fichiers occupé sans risquer la corruption.
6. Utiliser `force` uniquement en dernier recours sur NFS ou partitions corrompues.
7. Utiliser `/mnt` pour les montages systèmes et internes, et `/media/user` pour les périphériques amovibles détectés par l’interface graphique.

