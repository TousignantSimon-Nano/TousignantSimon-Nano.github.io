# Installation

Avant de pouvoir exécuter des scripts sur le ESP32 nous devons installer le pilote de périphérique pour communiquer avec le ESP et le logiciel Arduino IDE

## Installation des drivers CH340

Pour transérer notre code il faut installer le driver CH340 sur notre ordinateur. 

Commencez par connecter le ESP32 à l'ordinateur à l'aide du cable USB.

Ensuite téléchargez le driver à cette adresse : [https://www.wch-ic.com/search?q=CH340&t=downloads](https://www.wch-ic.com/search?q=CH340&t=downloads){target=_blank}. Le fichier à télécharger pour les portables sous Windows est **CH341SER.exe**. Exécutez le fichier une fois téléchargé.

Pour vérifier que le driver est bien installé, ouvrez l'explorateur de fichier et cliquez avec le bouton de droit sur "Ce PC". Sélectionnez ensuite "Gérer" et dans le paneau de droite "Gestionnaire de périphériques". 

![setup_01](\assets\images\esp32_setup_01.png){.center .shadow}

Dans la section "Ports (COM et LPT)" vous devriez avoir une entrée "USB-SERIAL CH340(COM4)". Le numéro du port peut changer (COM4).

## Installation de Arduino IDE

Passons maintenant à l'installation de notre IDE, Arduino IDE. Allez à l'adresse suivante télécharger la dernière version disponible pour votre système d'exploitation : 

- [https://www.arduino.cc/en/software](https://www.arduino.cc/en/software){target=_blank}

Démarrer l'installation une fois le programme téléchargé et ensuite lancez l'application.

![setup_02](\assets\images\esp32_setup_02.png){.center .shadow}

## Configuration de l'environnement

Encore quelques petites configurations. Dans le programme Arduino IDE, cliquez sur "Tools", "Board", "Board Manager" et "ESP32 by Expressif" 

![setup_03](\assets\images\Arduino_esp32_1_board_manager.png){.center .shadow}


Ensuite dans la barre en haut selectionner le drop-down Select Board and Port

![setup_04](\assets\images\Arduino_esp32_2_Select_Board_and_port.png){.center .shadow}

Spécifiez votre Port COM (varie d'un ordinateur à l'autre) et le modèle de board "ESP32 WROVER KIT"

![setup_05](\assets\images\Arduino_esp32_3_Select_Board.png){.center .shadow}

Bingo votre portable est connecté à votre ESP32, vous en avez la preuve ici

![setup_06](\assets\images\esp32_setup_05.png){.center .shadow}
