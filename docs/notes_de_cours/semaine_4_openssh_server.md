# Notes sur OpenSSH Server

## 1. Installation de OpenSSH Server

### Debian/Ubuntu :

``` bash
sudo apt update
sudo apt install openssh-server -y
```

------------------------------------------------------------------------

## 2. Position des fichiers de configuration

-   Fichier principal de configuration :\
    `/etc/ssh/sshd_config`

-   Fichier binaire du serveur :\
    `/usr/sbin/sshd`

-   Fichiers journaux (logs) :

    -   `/var/log/auth.log` (Debian/Ubuntu)\
    -   `/var/log/secure` (RHEL/CentOS/Fedora)

-   Clés hôtes (utilisées pour identifier le serveur) :\
    `/etc/ssh/ssh_host_*`

------------------------------------------------------------------------

## 3. Règles de sécurité essentielles

### Désactiver la connexion root

Dans `/etc/ssh/sshd_config`, modifier ou ajouter :

    PermitRootLogin no

#### Pourquoi désactiver Root ?

1.  **Réduire la surface d'attaque** : le compte `root` est connu de
    tous, donc facile à cibler.\
2.  **Traçabilité** : avec des comptes utilisateurs distincts, on sait
    qui fait quoi.\
3.  **Bonne pratique** : se connecter en tant qu'utilisateur normal puis
    utiliser `sudo` limite les dégâts en cas de piratage.

👉 **Alternative plus souple** :

    PermitRootLogin prohibit-password

Cela autorise root uniquement par clé SSH, mais pas par mot de passe.

------------------------------------------------------------------------

### Utiliser SSH protocol version 2

    Protocol 2

### Restreindre les utilisateurs autorisés

    AllowUsers user1 user2

ou

    AllowGroups sshusers

### Désactiver l'authentification par mot de passe (préférer les clés)

    PasswordAuthentication no

⚠️ Assurez-vous d'avoir configuré les clés SSH avant d'activer cette
règle.

### Timeout d'inactivité

    ClientAliveInterval 300
    ClientAliveCountMax 2

### Limiter le nombre de tentatives

    MaxAuthTries 3

### Recharger le service après modification

``` bash
sudo systemctl restart sshd
```

------------------------------------------------------------------------

## 4. Vérifier l'état du service

``` bash
systemctl status sshd
```

------------------------------------------------------------------------

## 5. Commandes utiles

-   Tester la configuration :

``` bash
sshd -t
```

-   Redémarrer le service :

``` bash
sudo systemctl restart sshd
```
