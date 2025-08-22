# Exercice 03 - Exploration Raspberry pi et Linux

Dans cet exercice on va aller un peu plus loin dans l'exploration de Raspberry Pi os. 

## Configuration initiale

### Installation de Raspberry Pi OS

- Sur une carte microSD installer {==Raspberry Pi OS Lite==} à l'aide de Raspberry Pi Imager sans effectuer de configuration avancée (Pas de création d'usager, de configuration du WiFi, etc.)

### Configuration au premier démarrage

Lors du premier démarrage, effectuer les configurations suivantes : 

- L'usager et le mot de passe.
- La langue du clavier.
- Ajuster le timezone sur `Montreal`.

## À faire

Notez dans un fichier texte les commandes, packages et logiciels que vous avez utilisés pour réaliser les points suivants.

### Configuration du Wifi

- Configurez le wifi (nmtui) pour les réseaux `Domotique-Pedago` et `TechInfo`. 
    - Affichez les interfaces réseaux du Pi.
	- Trouvez l'adresse de gateway
	- Trouvez la ou les adresses des serveurs DNS (Domain server)
	- Configurez une adresse ip fixe. Le professeur nous fournira l`adresse IP à utiliser. 
	- Configure le Default Gateway et le DNS pour l'adresse IP fixe
	- nmtui requiert un service network-manager restart

### SSH

- Activez SSH sur le PI
- Essayer de vous connecter depuis le terminal windows.

### Gestion des usagers

- Listez tous les usagers `cat /etc/passwd`
- Modifiez le nom et le mot de passe votre usager.
- Affichez les groups de permissions auxquels votre usager appartient.
- Ajoutez un nouvel usager.
- Changez d'utilisateur pour celui que vous venez de créer.
- Essayez de créer le fichier test.txt dans le répertoire /home de votre utilisateur principal.
- Donnez les permissions sudo à votre nouvel usager. 
- Refaite le test de créer un le fichier test.txt dans le répertoire /home de votre utilisateur principal.

### Mise à jour de packages

- Mettre à jour la liste des repository
- Appliquez les mise à jour si nécessaire
- Supprimez les fichiers non nécessaire qui ont été créés durant l'update
- Redémarrez le système

### Installation de package

- Installez tldr et le mettre à jour
	- Prenez le temps de tester la commande tldr
- Listez tous les packages installés
- Installez le package `SL` [https://itsfoss.com/ubuntu-terminal-train/](https://itsfoss.com/ubuntu-terminal-train/){target=_blank}
	- Créez un alias pour remplacer la commande ls par sl.
	- L'alias doit être persistant, redémarrer le pi pour le tester.
	- Maintenant vous pouvez supprimer l'alias.
	- Supprimer aussi l'application SL 
- Installez un des ces jeux pour prendre une petite pause : [https://itsfoss.com/best-command-line-games-linux/](https://itsfoss.com/best-command-line-games-linux/){target=_blank}

### Terminal virtuel

- Ouvrez un nouveau teminal virtuelle
- Basculer vers le premier.
- Fermez le deuxième terminal.

### Terminer un processus

- Lancez un des jeux que vous avez installé.
- Sans le quitter, ouvrez un nouveau terminal.
- Retrouvez le id du processus du jeu et terminez le.
- Fermez le terminal et revenez à celui de départ pour voir si le processus a bien été terminé.

### Brancher une clé usb (optionnel)

- Branchez une clé usb dans votre Pi et faites le nécessaire pour qu'elle soit "montée" sur le répertoire `/mnt/cle_usb`
- Essayer les deux méthodes décrites dans cet article : [https://raspberrytips.com/mount-usb-drive-raspberry-pi/](https://raspberrytips.com/mount-usb-drive-raspberry-pi/){target=_blank} Attention j'ai eu à changer les options de la commande `mount`

### Partage de fichier avec le Pi (optionnel)

Vous devez partager un répertoire de votre Pi pour que vous puissiez y accéder depuis votre portable sous Windows.

- Installez Samba
- Créez un répertoire shared à la racine de votre Pi `/shared` qui pourra être modifié par tous les usagers.
- Partager ce répertoire en lecture et écriture
- Créez aussi un deuxième partage pour la clé usb que vous avez montée plus tôt.
- Le tout devrait être accessible depuis votre portable (Connectez un lecteur réseau)
