# Notre premier sketch

## Un peu de mise en contexte

Les programmes qu'ont va écrire avec Arduino IDE sont appelées des sketches. Chaque programme va être enregistré dans un fichier portant l'extension **ino**. 

Pour compiler un sketch et en même temps vérifier qu'il ne contient pas d'erreur on va utiliser le bouton crochet, le raccourci Ctrl+R ou dans le menu "Sketch" et ensuite "Verify/Compile".

Pour envoyer un sketch sur le ESP32, cliquez sur le bouton avec la flèche, Ctrl+U ou bien dans le menu "Sketch" et ensuite "Upload".

Une fois le programme sur le ESP32, il va rouler en boucle tant que le ESP32 est sous tension. Pour l'instant la tension fournis par le cable USB est suffisante, mais on va voir plus tard qu'on doit parfois en fournir plus.

## Structure de nos programme

Parce que je vous aime et que je sais que vous êtes les meilleurs ont va programmer en C. La structure de nos programme sera sensiblement toujours la même.

1. En premier on va importer les librairies requises et déclarer les variables et objets globaux.
2. Ensuite nous avons la fonction `void setup()` qui va contenir du code d'initialisation et qui va être exécutée qu'un fois au démarrage.
3. Finalement il y a la fonction `void loop()` qui va être notre boucle de traitement principale. Cette fonction va tourner en boucle tant que le ESP32 est sous tension.
4. On peut aussi déclarer des fonctions à l'extérieur de "setup" et "loop" pour mieux structurer notre code.

## Premier petit test

Juste un petit programme tout mignon pour s'assurer que tout fonctionne. Dans Arduino IDE on a accès à un moniteur série dans lequel on peut écrire du texte depuis le ESP32. C'est pratique pour débugger ou simplement envoyer des communications. Nous faire un sketch qui va y inscrire du texte au démarrage.

1. Créez un nouveau sketch ("File" -> "New Sketch" ou bien Ctrl+N)
2. Inscrivez le code suivant : 

```c 
void setup() {
  // Initialise le port série à une vitesse de 9600 bauds
  Serial.begin(9600);
  // Affiche le texte Hello dans la console série et saute une ligne
  Serial.println("Hello");
}

// La fonction loop s'exécute à l'infini
void loop() {
  Serial.println("world!!");
  // Marque une pause de 1 seconde
  delay(1000);
}
```

## Enfin le sketch

Maintenant on va essayer de faire clignoter une petite DEL qui se situe sur le ESP32. 

![premier_sketch_01](/assets/images/premier_sketch_01.png){.center .shadow}

La DEL est associé au GPIO 2, il faut commencer par l'indiquer dans notre code en créant une constante contenant le numéro du GPIO. En fait cette étape n'est pas nécessaire mais simplifie le code quand on travail avec plusieurs "pins".

`#define PIN_DEL 2`

!!! note

        GPIO (General-Purpose Input/Output) sont des connecteurs, ou "pin", qui nous permettent de connecter le ESP32 à un circuit électrique. On peut les visualiser comme des interrupteurs qui peuvent être basculer "On" et "Off".

Ensuite on va initialiser la pin dans la fonction **setup()** et lui indiquer qu'elle va être en mode sortie, "OUTPUT".

`pinMode(PIN_DEL, OUTPUT);`

Un petit truc, ajoutez un délais à la fin de l'initialisation pour être sur que tout est chargé avant de se lancer dans la boucle de traitement.

Finalement pour allumer la DEL on va "écrire" dans la pin, on va lui envoyer un signal, HIGH pour l'allumer, LOW pour l'éteindre.

- Allume la DEL  : `digitalWrite(PIN_DEL, HIGH);`
- Etteind la DEL : `digitalWrite(PIN_DEL, LOW);` 

**À vous de jouer**

Assemblez tous ces morceaux de robots et écrivez un sketch qui va faire clignoter la DEL en continue à une intervalle de une seconde et demi. Quand la lumière allume inscrivez "On" dans le moniteur série et "Off" quand elle s'éteint.

**Ça fonctionne?**

Maintenant que vous avez une belle petite lumière qui clignote, modifiez votre code pour qu'après 10 clignotement la DEL s'éteingne et que dans le moniteur série on affiche le message "Ok c'est bon on a compris...". La DEL restera ensuite eteinte à moins qu'on redémarre le ESP32.
