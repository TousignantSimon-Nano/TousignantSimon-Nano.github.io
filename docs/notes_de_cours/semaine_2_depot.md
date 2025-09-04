# Gestion des paquets avec APT

APT (**Advanced Package Tool**) est le gestionnaire de paquets utilisé
par les distributions basées sur **Debian** (Ubuntu, Linux Mint, etc.).\
Il permet de rechercher, installer, mettre à jour et supprimer des
logiciels.

------------------------------------------------------------------------

## 1. Commandes de base

### Mettre à jour la liste des paquets

``` bash
sudo apt update
```

-   Cette commande **ne met pas à jour les logiciels**.\
-   Elle télécharge la liste des paquets disponibles à partir des dépôts
    configurés dans `/etc/apt/sources.list` et
    `/etc/apt/sources.list.d/`.\
-   Résultat : le système sait quelles nouvelles versions sont
    disponibles.

### Mettre à jour les logiciels installés

``` bash
sudo apt upgrade
```

-   Installe les **nouvelles versions** des paquets déjà installés (sans
    supprimer ni installer de nouveaux paquets).

Pour des mises à jour plus profondes (qui peuvent installer/supprimer
des dépendances) :

``` bash
sudo apt full-upgrade
```

### Installer un paquet

``` bash
sudo apt install nom-du-paquet
```

Exemple :

``` bash
sudo apt install vim
```

------------------------------------------------------------------------

## 2. Fichiers et dossiers importants

-   `/etc/apt/sources.list`\
    → Contient la liste principale des dépôts de logiciels.

-   `/etc/apt/sources.list.d/`\
    → Répertoire contenant des fichiers `.list` pour des dépôts
    additionnels (souvent ajoutés manuellement ou par un logiciel
    tiers).

-   `/var/lib/apt/lists/`\
    → Contient les fichiers téléchargés par `apt update` (les index de
    paquets).

-   `/etc/apt/trusted.gpg` et `/etc/apt/trusted.gpg.d/`\
    → Contiennent les **clés GPG** permettant de vérifier l'authenticité
    des paquets téléchargés.

------------------------------------------------------------------------

## 3. Ajouter un dépôt

### Exemple : ajouter le dépôt officiel de Docker

1.  Ajouter la clé GPG du dépôt :

``` bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker.gpg
```

2.  Ajouter le dépôt dans `/etc/apt/sources.list.d/` :

``` bash
echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" | sudo tee /etc/apt/sources.list.d/docker.list
```

3.  Mettre à jour la liste des paquets :

``` bash
sudo apt update
```

4.  Installer le paquet :

``` bash
sudo apt install docker-ce
```

------------------------------------------------------------------------

## 4. Les clés GPG et la validation des dépôts

-   Chaque dépôt signe ses paquets avec une **clé privée**.\
-   Ton système stocke la **clé publique** correspondante dans
    `/etc/apt/trusted.gpg.d/`.\
-   Quand tu télécharges un paquet, `apt` vérifie la signature → si elle
    ne correspond pas, le paquet est rejeté (erreur *NO_PUBKEY*).

### Ajouter une clé manuellement

Si un dépôt te demande d'ajouter une clé :

``` bash
wget -qO - https://example.com/repo.gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/example.gpg
```

### Vérifier les clés connues

``` bash
apt-key list
```

*(À noter : `apt-key` est en voie d'abandon, la méthode recommandée est
l'usage de fichiers `.gpg` dans `/etc/apt/trusted.gpg.d/`.)*

------------------------------------------------------------------------

## 5. Exemple pratique

Ajout du dépôt **Google Chrome** :

``` bash
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/google.gpg

echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" | sudo tee /etc/apt/sources.list.d/google-chrome.list

sudo apt update
sudo apt install google-chrome-stable
```

------------------------------------------------------------------------

## 6. Résumé visuel

-   `apt update` → met à jour la liste des paquets depuis les dépôts.\
-   `apt upgrade` → met à jour les paquets installés.\
-   `apt install` → installe un paquet.\
-   Dépôts listés dans : `/etc/apt/sources.list` et
    `/etc/apt/sources.list.d/`.\
-   Clés de vérification : `/etc/apt/trusted.gpg.d/`.

------------------------------------------------------------------------

# Gestion des paquets avec APT -- Commandes complémentaires

En plus de `update`, `upgrade` et `install`, APT propose d'autres
commandes très utiles pour gérer les logiciels installés ou disponibles
sur le système.

------------------------------------------------------------------------

## 1. Lister les paquets

### Lister tous les paquets disponibles

``` bash
apt list
```

-   Affiche tous les paquets connus du système (installés ou non).
-   Liste très longue → généralement on combine avec `grep`.

Exemple :

``` bash
apt list | grep python3
```

### Lister uniquement les paquets installés

``` bash
apt list --installed
```

### Lister les paquets pouvant être mis à jour

``` bash
apt list --upgradable
```

------------------------------------------------------------------------

## 2. Rechercher des paquets

### Rechercher par nom ou description

``` bash
apt search mot-clef
```

Exemple :

``` bash
apt search editor
```

→ Affiche tous les paquets dont le nom ou la description contient
*editor*.

------------------------------------------------------------------------

## 3. Supprimer des paquets

### Supprimer un paquet sans toucher à ses fichiers de configuration

``` bash
sudo apt remove nom-du-paquet
```

Exemple :

``` bash
sudo apt remove vim
```

### Supprimer un paquet **et ses fichiers de configuration**

``` bash
sudo apt purge nom-du-paquet
```

Exemple :

``` bash
sudo apt purge vim
```

------------------------------------------------------------------------

## 4. Gestion automatique des dépendances

Quand on installe un logiciel, APT installe souvent d'autres paquets
nécessaires (**dépendances**).\
Si ces dépendances ne sont plus utilisées, on peut les supprimer
automatiquement.

### Supprimer les paquets installés automatiquement et devenus inutiles

``` bash
sudo apt autoremove
```

-   Nettoie le système.\
-   Exemple : si on désinstalle `libreoffice`, certains paquets
    dépendants peuvent rester → `autoremove` les supprime.

### Exemple pratique

1.  Installez `geany` :

    ``` bash
    sudo apt install geany
    ```

    → plusieurs bibliothèques sont installées en plus.

2.  Supprimez `geany` :

    ``` bash
    sudo apt remove geany
    ```

    → certaines dépendances restent installées.

3.  Vérifiez les paquets devenus inutiles :

    ``` bash
    sudo apt autoremove
    ```

------------------------------------------------------------------------

## 5. Exemples pratiques

-   Lister les paquets liés à Python :

    ``` bash
    apt list --installed | grep python3
    ```

-   Rechercher un navigateur dans les dépôts :

    ``` bash
    apt search browser
    ```

-   Supprimer Firefox et nettoyer les dépendances :

    ``` bash
    sudo apt remove firefox
    sudo apt autoremove
    ```

------------------------------------------------------------------------

## 6. Résumé visuel

-   `apt list` → liste les paquets (installés, disponibles, à mettre à
    jour).\
-   `apt search` → recherche un paquet.\
-   `apt remove` → supprime un paquet (mais garde les fichiers de
    config).\
-   `apt purge` → supprime un paquet + ses fichiers de config.\
-   `apt autoremove` → supprime les dépendances inutiles.
