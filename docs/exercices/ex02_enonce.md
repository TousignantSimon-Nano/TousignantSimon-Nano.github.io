# Exercice 02 - RetroPie

Pour notre premier projet avec un raspberry Pi on va le transformer en plate-forme de rétrogaming avec la distribution RetroPie.
![RetroPieLogo](\assets\images\RetroPieLogo.png){.center}


## Objectifs

## Matériel requis

- Un raspberry Pi
- [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
- Une carte microSD
- Une manette de jeu USB

## Marche à suivre

### Installer RetroPie

Utilisez le logiciel Raspberry Pi Imager pour faire l'installation. Au lieu de choisir RetroPie dans la liste des OS disponibles utilisez l'image que je vais vous fournir. Vous pouvez aussi la télécharger ici : [liens](https://retropie.org.uk/download/) 

!!! danger 

    Conservez le nom d'usager (`pi`) et le mot de passe (`raspberry`) par défaut lors de l'installation de l'image de RetroPie sinon l'installation ne se fera pas correctement.

### Configuration

#### Manette
Insérez la carte SD dans le pi, branchez la manette de jeu et lancez le système. Suivez les instructions à l'écran pour configurer la manette.

#### Wifi

Sélectionnez configuration dans le menu et ensuite Wifi. 

Vous devrez indiquer le WLAN COUNTRY, suivez les étapes dans Localisation Options > WLAN Country > Canada

Le réseau wifi qu'on va utiliser est `Domotique-Pedago`, je vais vous donner le mot de passe en classe. Notez l'adresse ip de votre Pi.

#### Mise à jour

Faites la mise à jour de votre installation. Il y a une option dans le menu de configuration, je vous laisse chercher un peu.

#### Activez SSH

On va transférer nos jeux via SSH. Par défaut il est désactivé sur Retropie, vous devez trouver comment le réactiver. Maintenant vous pouvez vous connecter à votre pi avec un client SSH, moi j'utilise [Putty](https://www.putty.org/){target=_blank}

#### Transférer des jeux

Je vous ai préparé une petite sélection de jeux NES que vous pouvez télécharger [ici](\assets\files\ex02_nes_roms.zip). Avec Retropie les jeux doivent être copiés dans le répertoire correspondant à leur plateforme. Dans notre cas ce sera le répertoire `/home/pi/RetroPie/roms/nes`. Il y a plusieurs façons de transférer les fichiers. Étant donné que le SSH est activé sur le pi, je veux que vous utilisiez {==scp==} ou {==sftp==} en console.

#### Changez l'écran de démarrage

Changez l'écran de démarrage de Retropie. Vous pouvez utiliser une des images ou vidéos fournies ou pour aller plus loin importer votre propre image.

## Jouez!!

C'est maintenant le temps de tester votre machine de rétrogaming, amusez-vous.

## Ressources 

- [Documentation de Retropie](https://retropie.org.uk/docs/){target=_blank}
