# Emulateur de Sense Hat

Il existe des émulateurs de Sense Hat qui nous permet de créer des scripts et d'interragir avec les capteurs sans avoir besoin de posséder la carte physiquement. 

Vous pouvez en trouver un en ligne à l'adresse [https://trinket.io/sense-hat](https://trinket.io/sense-hat). L'interface est assez simple. Vous écrivez votre code en python à gauche et vous avez l'émulation du Sense Hat à droite.

![Sense Hat Emulateur](\assets\images\sense_hat_02.png){.center .shadow}

-----------------------

Vous avez accès dans à une version de l'émulateur dans le système d'exploitation Pi OS généralement installé sur un Raspberry Pi. 

![Sense Hat Emulateur](\assets\images\sense_hat_03.png){.center .shadow}

Il n'est par contre pas installé par défaut dans la version lite ou régulière. Si vous avez à installer Pi OS, sélectionnez la version full. Sinon il est toujours possible d'installer l'émulateur sur une installation déjà existante avec les commandes : 

NOTES SEPT 2024: ne fonctionne pas avec la version actuelle de Pi OS (v12 - Bookworm) - utiliser la version [en ligne](https://trinket.io/sense-hat)

``````bash
sudo apt-get update
sudo apt-get install python-sense-emu python3-sense-emu sense-emu-tools
``````

!!! Attention

        Si vous développez avec l'émulateur, vos scripts python doivent importer sense_emu au lieu de sense_hat

        `from sense_emu import SenseHat`



## Source 

- [Emulateur en ligne](https://trinket.io/sense-hat){target=_blank}
- [Sense-emu](https://sense-emu.readthedocs.io/en/v1.1/index.html){target=_blank}
