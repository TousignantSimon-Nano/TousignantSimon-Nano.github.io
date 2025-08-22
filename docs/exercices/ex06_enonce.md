# Exercice 06 - Une DEL qui clignote

Vous devez produire un sketch Arduino pour l'ESP32 qui va exécuter les points suivants:

1. Vous devez faire clignoter la DEL du ESP32 selon la fréquence que vous désirez.
2. Démarrer le clignotement de la LED ou arrêter-le en envoyant une commande par le port série. `ON` pour démarrer et `OFF` pour l'arrêter.
3. Ajoutez une troisième commande qui va permettre d'ajuster le temps d'attente entre les clignotements de la DEL. La commande sera DELx où x représente un entier en millisecondes. (`DEL1500` par exemple).
4. Quand vous envoyez une des trois commandes elle doivent être appliquées immédiatement au traitement. Par exemple si la DEL est allumée, clignote sur un intervalle de 2 secondes et que vous lancer la commande OFF elle devra s'éteindre aussitôt. Utilisez la bonne méthode pour gèrer le temps d'attente.

Indices
- Ne pas utiliser delay()
- Serial.setTimeout()

Quand vous avez terminé montrez-moi fièrement votre résultat.
