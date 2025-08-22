# Afficher sur un pixel

La matrice de DEL présente sur le Sense Hat est en fait une série de 64 LED indépendante. On peut faire un affichage en utilisant que les DELs souhaités. On peut donc cibler une DEL en particulier en donnant ses coordonnées en x et en y. Les lignes sont numérotées de haut en bas de 0 à 7 et les colonnes de gauche à droite de 0 à 7 aussi. Donc la première DEL en haut à gauche à les coordonnées 0,0.

La commande est `set_pixel(x, y, color)` où color représente un tuple de couleur RGB.

``````python linenums="1"
from sense_emu import SenseHat
sense = SenseHat()

# Déclaration des couleurs
rose = (255,0,255)
blanc = (255,255,255)

# Colore le pixel à la position 2,3 en rose.
sense.set_pixel(2,3,rose)
``````

Ok maintenant je suis sur que vous voulez faire du "pixel art" avec le Sense Hat. Et bien sachez qu'il existe aussi la commande `set_pixels` qui nous permet de colorer toutes les DELs. La commande prend en paramètres une liste de couleur RGB (la liste commence en haut à gauche et se déroule ligne par ligne). Attention, la liste doit comporter les 64 couleurs.

<iframe src="https://trinket.io/embed/python/603006f3b3" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

L'exemple provient de se site : [https://projects.raspberrypi.org/en/projects/getting-started-with-the-sense-hat/5](https://projects.raspberrypi.org/en/projects/getting-started-with-the-sense-hat/5){target=_blank}


