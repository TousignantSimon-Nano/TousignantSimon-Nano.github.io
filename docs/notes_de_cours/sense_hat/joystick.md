# Utilisation du joystick

Le Sense Hat possède aussi un joystick qui nous permet de capter les touches haut, bas, gauche, droite ainsi qu'un clic. Ces touches sont aussi "mappé" sur le clavier avec les flèches de directions et le clic par la touche entrée. Quand une direction est détectée, un évènement est lancé et est stocké dans un objet "event". Pour capter ces évènements, on va dans notre boucle de traitement on va aller chercher les évènements avec la commande `sense.stick.get_events()`. Ensuite on pourra utiliser les propriétés suivantes de l'objet "event": 

- direction : Obtenir la direction, donc la touche pressée (up, down, left, right, middle). Middle représente le clic.
- action : Pour savoir si la touche est pressée ou relâchée (pressed, released).

Exemple, je veux déclencher un traitement lorsque je clique sur le joystick : 

``````python linenums="1"
from sense_emu import SenseHat
sense = SenseHat()

while True:
    for event in sense.stick.get_events():
        # Je vérifie qu'il y a clic du joystick 
	# Attention appelé quand appuyé ET quand relaché
        if event.direction == "middle":
            # Mon traitement
            
``````

## Écouter un événement du joystick

Il est aussi possible de "brancher" un événement du joystick à une fonction. Chaque direction à une propriété associée à laquelle on donne la fonction: 

- `sense.stick.direction_up`
- `sense.stick.direction_down`
- `sense.stick.direction_left`
- `sense.stick.direction_right`
- `sense.stick.direction_middle`


``````python linenums="1" title="Exemple d'utilisation"
from sense_emu import SenseHat
sense = SenseHat()

rouge = (255, 0, 0)

def point_rouge():
    sense.set_pixel(4,4,rouge)

# On associe la fonction point_rouge au clic
sense.stick.direction_middle = point_rouge

while True:
    # Ici le pass sert uniquement à rester dans la boucle
    # dès que le bouton sera appuyé la fonction va être lancée.
    pass
            
``````
