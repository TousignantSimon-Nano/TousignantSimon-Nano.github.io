# Les capteurs du Sense Hat

Comme nous l'avons vu, le Sense Hat possède plusieurs capteurs et la méthode pour récupérer les informations est assez simple: 

``````python linenums="1" title="Exemple valeur capteurs"
from sense_emu import SenseHat
sense = SenseHat()

# Valeur du capteur d'humidité
humidite = sense.get_humidity()
# Valeur du capteur de pression
pression = sense.get_pressure()
# Valeur du capteur de température
temperature = sense.get_temperature()
``````
Parcontre dans cette exemple la lecture n'est prise qu'une fois. Si on voudrais avoir une lecture en continue on devrait utiliser une boucle de traitement.

La température peut être prise à la fois par le capteur d'humidité et le capteur de pression. Il y a une fonction pour lire sur chacun d'eux : 

``````python linenums="1" title="Exemple capteur température"
from sense_emu import SenseHat
sense = SenseHat()

# Température provenant du capteur d'humidité
temp_humidite = sense.get_temperature_from_humidity()
# Température provenant  du capteur de pression
temp_pression = sense.get_temperature_from_pressure()
``````

La commande `sense.get_temperature()` est un raccourci de la commande `sense.get_temperature_from_humidity()`

Dans l'émulateur de Sense Hat on peut simuler les valeurs lues par chaque capteur en jouant avec les barres défilantes.
