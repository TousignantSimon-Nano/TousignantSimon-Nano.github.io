# Gestion réseau sur Raspberry Pi OS Bookworm (Debian 12) – Version détaillée avec fichiers

---

## 1. Généralités
- Gestionnaire réseau : **NetworkManager**
- CLI : `nmcli`
- Interface console semi-graphique : `nmtui`
- Fichiers de configuration importants :
  - Connexions : `/etc/NetworkManager/system-connections/` (fichiers `.nmconnection`)
  - Paramètres globaux : `/etc/NetworkManager/NetworkManager.conf`

---

## 2. Fichiers de configuration – exemples

### a) Ethernet en DHCP
Fichier : `/etc/NetworkManager/system-connections/Bureau.nmconnection`
```ini
[connection]
id=Bureau
type=ethernet
interface-name=eth0
permissions=

[ethernet]
mac-address-blacklist=

[ipv4]
method=auto

[ipv6]
method=ignore
```

### b) Ethernet en IP statique
Fichier : `/etc/NetworkManager/system-connections/BureauStatique.nmconnection`
```ini
[connection]
id=BureauStatique
type=ethernet
interface-name=eth0
permissions=

[ethernet]
mac-address-blacklist=

[ipv4]
method=manual
addresses1=192.168.1.100/24,192.168.1.1
dns=8.8.8.8;8.8.4.4;

[ipv6]
method=ignore
```

### c) Wi-Fi en DHCP
Fichier : `/etc/NetworkManager/system-connections/Maison.nmconnection`
```ini
[connection]
id=Maison
type=wifi
interface-name=wlan0
permissions=

[wifi]
ssid=Maison
mode=infrastructure

[wifi-security]
key-mgmt=wpa-psk
psk=12345678

[ipv4]
method=auto

[ipv6]
method=ignore
```

### d) Wi-Fi en IP statique
Fichier : `/etc/NetworkManager/system-connections/MaisonStatique.nmconnection`
```ini
[connection]
id=MaisonStatique
type=wifi
interface-name=wlan0
permissions=

[wifi]
ssid=Maison
mode=infrastructure

[wifi-security]
key-mgmt=wpa-psk
psk=12345678

[ipv4]
method=manual
addresses1=192.168.1.50/24,192.168.1.1
dns=8.8.8.8;

[ipv6]
method=ignore
```

---

## 3. Commandes de gestion réseau

### a) Vérifier l’état des interfaces
```bash
nmcli device status
```

### b) Liste des connexions connues
```bash
nmcli connection show
```

### c) Connexion Wi-Fi rapide (DHCP)
```bash
nmcli device wifi connect "NomDuSSID" password "motdepasse"
```

### d) Connexion Ethernet (IP statique)
```bash
nmcli connection add type ethernet con-name "BureauStatique" ifname eth0 \
ipv4.method manual ipv4.addresses 192.168.1.100/24 ipv4.gateway 192.168.1.1 \
ipv4.dns 8.8.8.8
nmcli connection up "BureauStatique"
```

### e) Interface semi-graphique
```bash
sudo nmtui
```
- Créer / modifier / activer des connexions Wi-Fi et Ethernet  

---

## 4. Notes pratiques pour les étudiants

1. Les fichiers `.nmconnection` **sont propriétaires root**, modification avec `sudo nano` si nécessaire.  
2. Après modification d’un fichier, toujours **recharger la connexion** :
```bash
nmcli connection reload
nmcli connection up "NomDeLaConnexion"
```
3. `nmtui` simplifie la création de connexion sans éditer les fichiers.  
4. Toujours vérifier la connectivité avec :
```bash
ping 8.8.8.8
ping google.com
```

---

## 5. Comparatif DHCP vs IP statique

| Critère               | DHCP                        | IP statique                       |
|-----------------------|-----------------------------|----------------------------------|
| Attribution IP        | Automatique par routeur     | Fixe, définie manuellement       |
| Facilité              | Très simple                 | Plus complexe                     |
| Utilité               | Postes clients              | Serveurs, IoT, Raspberry Pi fixes |
| Modification réseau   | Transparente                | Nécessite mise à jour manuelle   |

