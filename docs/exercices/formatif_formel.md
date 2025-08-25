# Formatif formel

L'objectif de ce formatif est d'installer et de configurer un serveur de musique sur votre Pi et de me permettre de contrôler le serveur depuis un navigateur sur mon portable. Le serveur que nous allons installer se nomme Mopidy.

## Installation et configuration du système d'exploitation

- Installez **Raspberry Pi OS Lite (32-bit)** à l'aide de Raspberry Pi Imager sans faire aucune configuration.
- Configurez depuis le terminal du pi: 
    - L'usager et le mot de passe.
    - La langue du clavier.
    - Le timezone : `Montreal`.
    - Activez le SSH.
    - Modifier la sortie audio pour la prise 3.5mm

## Configuration du wifi et adresse ip fixe

- Configurez le wifi (raspi-config) pour le réseau `Domotique-Pedago`. 
	- Trouvez la ou les adresses des serveurs DNS (Domain server)
    - Trouvez l'adresse de gateway
    - Configurez une adresse ip fixe. Utilisez le numéro de votre pi comme dernier octet de l'adresse ip.

## Installation de Mopidy

Installez Mopidy sur votre Pi, vous pouvez trouver les instructions d'installation ici: [Installation Mopidy](https://docs.mopidy.com/en/latest/installation/raspberrypi/){target=_blank}

## Lancement de Modipy

Configurez Modipy pour qu'il soit lancé comme un service. [Documentation](https://docs.mopidy.com/en/latest/running/){target=_blank}

## Configuration de Mopidy-HTTP

Configurez l'extension pour qu'on puisse accéder à Modipy depuis le protocole HTTP. Dans le fichier de configuration le `hostname` sera votre adresse ip fixe. [Documentation](https://docs.mopidy.com/en/latest/ext/http/){target=_blank}

## Configuration de Mopidy-Local

- Créez un répertoire `musik` dans votre `/home/[user]`
- Configurez Mopidy-File pour que ce répertoire soit listé : [Documentation](https://github.com/mopidy/mopidy-local){target=_blank}

## Récupération d'un fichier audio

Connectez-vous sur mon pi pour récupérer le fichier `the_mexican_hat_dance.mp3` et copiez ensuite ce fichier dans votre répertoire `musik`

- Adresse ip : 172.19.240.99
- User : invite
- Password : formatif


## Installation du client Iris

- Installez le client Iris pour que je puisse contrôler Modipy depuis mon portable.
- [Documentation](https://mopidy.com/ext/iris/){target=_blank}

## Correction

Lorsque vous êtes prêt, je dois pouvoir faire jouer le fichier mp3 depuis un navigateur sur mon portable. Ensuite dans un répertoire compressé portant le nom **nom_prenom_ff**, je veux avoir les fichiers suivants : 

- Votre fichier `dhcpcd.conf`
- Votre fichier de configuration `mopidy.conf`

Remettez-moi le fichier dans le devoir sur Teams

## Grille de correction

| Critères                                                 |  Points |
| -------------------------------------------------------- | ------: |
|                                                          |         |
| Installation et configuration du système d'exploitation  |       5 |
| Configuration du wifi et adresse ip fixe                 |       5 |
| Installation de Mopidy en service                        |       5 |
| Configuration de Mopidy-HTTP                             |       5 |
| Configuration de Mopidy-Local                            |       5 |
| Récupération d'un fichier audio                          |       5 |
| Installation du client Iris                              |       5 |
| Remise des fichiers dans un format compressé             |       5 |
| On peut faire jouer une chanson depuis un autre portable |      10 |
|                                                          | **/50** |
