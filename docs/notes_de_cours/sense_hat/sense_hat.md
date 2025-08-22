# Sense Hat

Le Sense Hat est un carte d'extension que l'on branche sur un Raspberry Pi (HAT est une abbréviation qui signifie "Hardware Attached on Top") pour étendre ses fonctionnalitées grâce à une série de capteurs: 

- Accéléromètre:  pour obtenir l'accélération du Pi, en calculer la vitesse et la position dans l'espace
- Gyroscope: pour capturez le mouvement de rotation du Raspberry Pi
- Magnétomètre: pour mesurer du champ magnétique
- Capteur de pression d’air
- Capteurs de température et d’humidité

Pour terminer, le Sense Hat possède une matrice de LED 8x8 et un mini-joystick.

![Sense Hat](\assets\images\sense_hat_01.png){.center}

!!! Info

        À l'origine le Sense Hat se nommait "Astro Pi" et avait été développé dans l'objectif d'envoyer des Raspberry Pi avec capteurs à bord de la Station spatiale internationale (ISS).


# Emulateur de Sense Hat

Il existe des émulateurs de Sense Hat qui nous permet de créer des scripts et d'interagir avec les capteurs sans avoir besoin de posséder la carte physiquement. 

Vous pouvez en trouver un en ligne à l'adresse [https://trinket.io/sense-hat](https://trinket.io/sense-hat){target=_blank}. L'interface est assez simple. Vous écrivez votre code en python à gauche et vous avez l'émulation du Sense Hat à droite.

![Sense Hat Emulateur](\assets\images\sense_hat_02.png){.center .shadow}

Vous avez accès dans à une version de l'émulateur dans le système d'exploitation Pi OS généralement installé sur un Raspberry Pi. Il n'est par contre pas installé par défaut dans la version lite ou régulière. Si vous avez à installer Pi OS, sélectionnez la version full. Sinon il est toujours possible d'installer l'émulateur sur une installation déjà existante avec les commandes : 

``````bash
sudo apt-get update
sudo apt-get install python-sense-emu python3-sense-emu sense-emu-tools
``````

*NOTES SEPT 2024*: ne fonctionne pas avec la version actuelle de Pi OS (v12 - Bookworm) - utiliser la version [en ligne](https://trinket.io/sense-hat)

!!! Attention

        Si vous développez avec l'émulateur, vos scripts python doivent importer sense_emu au lieu de sense_hat

        `from sense_emu import SenseHat`



## Source 

- [https://projects.raspberrypi.org/en/projects/getting-started-with-the-sense-hat/0](https://projects.raspberrypi.org/en/projects/getting-started-with-the-sense-hat/0){target=_blank}
