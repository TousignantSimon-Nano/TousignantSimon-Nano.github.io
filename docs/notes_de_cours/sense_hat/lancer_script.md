# Interragir avec le Sense Hat

Il existe une librairie python pour travailler avec le Sense Hat. Étant donnée qu'on n'utilisera pas sa version physique nous n'avons pas à installer cette librairie.

Le langage à utiliser pour interragir avec Sense Hat est python. Dès que le carte physique est bien branché au Raspberry Pi (on dans notre cas l'émulateur est lancé), le Sense Hat est disponible.

Nos scripts débuteront avec l'importation de la librairie. 

``````python title="Importation de la librairie"
# Si on utilise une carte Sense Hat 
from sense_hat import SenseHat
# Si on utilise l'émulateur 
from sense_emu import SenseHat
``````

## Utilisation de la librairie

Après avoir importé la librairie, on va créer un objet SenseHat avec lequel on va travailler.

``````python
# Création d'un objet SenseHat 
sense = SenseHat()
``````

## Afficher du texte

Il y a deux commandes qui nous permettent d'afficher du texte facilement sur la série de DEL.

- `show_message()` : Qui nous permet d'afficher une chaine de texte, elle sera affiché en mouvement de droite à gauche. Le texte va disparaitre ensuite.
- `show_letter()` : Affiche seulement un caractère. Parcontre le caractère reste affiché à l'écran tant qu'on n'affiche rien d'autre.

!!! astuce

        On peut aussi à tout moment effacer l'écran avec la commande `sense.clear()`

``````python linenums="1" title="Exemple de script Hello world"
from sense_emu import SenseHat
sense = SenseHat()

sense.show_message("Hello World")
``````

## Boucle de traitement

Quand le script est lancé sur le Sense Hat, il est exécuté qu'une fois et ensuite s'arrête. Dans la grande majorité des cas ce n'est pas le comportement que l'on souhaite, surtout quand on va travailler avec les capteurs. Onn va donc prendre l'habitude de placer notre code dans une boucle de traitement qui va s'exécuter tant que le Sense Hat est sous tension. En python le plus simple est de faire une boucle infinie avec `while true` : 

``````python linenums="1" title="Exemple de boucle"
from sense_emu import SenseHat
sense = SenseHat()

while True:
    sense.show_message("Hello World")
``````
## Utilisation de la commande sleep pour stopper le traitement

Selon le traitement il peut être nécessaire de stopper le traitement de la boucle. Par exemple je veux afficher les chiffres de 1 à 3 en continue.

``````python linenums="1"
from sense_emu import SenseHat
sense = SenseHat()

while True:
    sense.show_letter("1")
    sense.show_letter("2")
    sense.show_letter("3")
``````

Si je lance ce code, je vais n'avoir que le chiffre 3 d'affiché en permanence. Pourquoi? Parce qu'à chaque itération de la boucle, les trois chiffres sont affiché trop rapidement pour le voir à l'oeil et au final on ne voit que le dernier.

La solution est de ralentir le traitement avec la commande sleep de python. Pour l'utiliser il faut importer la librairie time : 

``````python
from time import sleep
``````

Ensuite la commande `sleep` prend un nombre de seconde en paramètre qui correspond au temps d'arrêt voulu. Ce nombre peut être décimal. Reprenons le même exemple mais cette fois avec la commande sleep : 

``````python linenums="1"
from sense_emu import SenseHat
sense = SenseHat()

while True:
    sense.show_letter("1")
    sleep(0.5)
    sense.show_letter("2")
    sleep(0.5)
    sense.show_letter("3")
    sleep(0.5)
``````

Maintenant les chiffres vont défiler l'un après l'autre avec un intervalle de 0.5 seconde.