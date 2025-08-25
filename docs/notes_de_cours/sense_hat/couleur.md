# Mettre un peu de couleur

On a déjà vu qu'avec les commandes show_message et show_letter ont peut afficher des caractères. On peut aussi ajouter des paramètre pour modifier la couleur.

Les couleurs seront exprimées en RGB sous forme de tuple : (255,255,255) pour du blanc par exemple. Les deux commandes vont prendre en paramètre la couleur du texte et la couleur du fond (optionnelle).

``````python linenums="1"
from sense_emu import SenseHat
sense = SenseHat()

# Affiche le message Hello World en rose sur fond blanc.
sense.show_message("Hello World", (255,0,255), (255,255,255))
``````

Question de simplifier le code on peut mettre nos tuples de couleurs dans des variables qu'on réutilise au besoin : 

``````python linenums="1"
from sense_emu import SenseHat
sense = SenseHat()

# Déclaration des couleurs
rose = (255,0,255)
blanc = (255,255,255)

# Affiche le message Hello World en rose sur fond blanc.
sense.show_message("Hello World", rose, blanc)
``````

On peut aussi directement nommer le paramètre et lui donner la valeur. Le nom des paramètre est `text_colour` et `back_colour`. Par exemple je veux changer la couleur de fond de mon message mais conserver la couleur du texte par défaut.
``````python linenums="1" title="Exemple de script Hello world"
from sense_emu import SenseHat
sense = SenseHat()

# Déclaration des couleurs
rose = (255,0,255)

# Affiche le message Hello World en rose sur fond blanc (couleur de fond par defaut).
sense.show_message("Hello World", text_colour=rose)
``````

On peut aussi utiliser la commande `clear` pour appliquer une couleur à toutes les DELs

``````python linenums="1" title="Exemple de script Hello world"
from sense_emu import SenseHat
sense = SenseHat()

# Déclaration des couleurs
rose = (255,0,255)
bleu = (0,0,255)

# Affiche le message Hello World en rose sur fond blanc.
sense.show_message("Hello World", text_colour=rose)
# Ensuite l'écran devient tout bleu
sense.clear(bleu)
``````
