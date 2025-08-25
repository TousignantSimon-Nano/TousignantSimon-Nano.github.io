# Faire une pause dans le traitement

Parfois on veut pouvoir faire une pause dans le traitement de notre sketch. Le code étant placé dans une boucle infini qui tourne rapidement, est-ce que nous avons vraiment besoin de prendre une mesure de la température à toute les x millisecondes? Bien sur que non, et il y a des façon de ralentir le traitement.

## La méthode avec delay()

Comme nous l'avons déjà vu, on peut utiliser la fonction `delay()` qui prend en paramètre un nombre de millisecondes d'attente.

```c
// Marque une pause de 1 seconde
delay(1000)
```

Le désavantage de cette méthode est que {==tout le traitement==} est stoppé durant ce délai.

## La méthode plus flexible

On ne peut pas récupérer le temps actuelle depuis le ESP32 mais un peu parcontre savoir depuis combien de temps le programme actuelle tourne sur le ESP32. 

La fonction `millis()` va nous retourner se nombre en millisecondes.

L'idée est de définir une variable initialisée à 0 et qui va contenir le moment où la dernière exécution du traitement qu'on veut retarder. On va aussi se définir une intervalle en millisecondes qui va représenter notre temps d'attente. 

Maintenant à chaque itération de la boucle de traitement, on va récupérer le temps avec `millis()`. Ensuite si le temps récupéré - le moment de la dernière exécution est sépérieur ou égale à notre intervalle prédéfinie et va lancer le traitement. On va aussi attribuer à notre variable qui contenait le moment de la dernière exécution la valeur du temps actuelle.

Voici un petit exemple tiré de la documentation d'Arduino. 

```c linenums="1"
/*
  Blink without Delay

  Turns on and off a light emitting diode (LED) connected to a digital pin,
  without using the delay() function. This means that other code can run at the
  same time without being interrupted by the LED code.

  The circuit:
  - Use the onboard LED.
  - Note: Most Arduinos have an on-board LED you can control. On the UNO, MEGA
    and ZERO it is attached to digital pin 13, on MKR1000 on pin 6. LED_BUILTIN
    is set to the correct LED pin independent of which board is used.
    If you want to know what pin the on-board LED is connected to on your
    Arduino model, check the Technical Specs of your board at:
    https://www.arduino.cc/en/Main/Products

  created 2005
  by David A. Mellis
  modified 8 Feb 2010
  by Paul Stoffregen
  modified 11 Nov 2013
  by Scott Fitzgerald
  modified 9 Jan 2017
  by Arturo Guadalupi

  This example code is in the public domain.

  https://www.arduino.cc/en/Tutorial/BuiltInExamples/BlinkWithoutDelay
*/

// constants won't change. Used here to set a pin number:
const int ledPin = LED_BUILTIN;  // the number of the LED pin

// Variables will change:
int ledState = LOW;  // ledState used to set the LED

// Generally, you should use "unsigned long" for variables that hold time
// The value will quickly become too large for an int to store
unsigned long previousMillis = 0;  // will store last time LED was updated

// constants won't change:
const long interval = 1000;  // interval at which to blink (milliseconds)

void setup() {
  // set the digital pin as output:
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // here is where you'd put code that needs to be running all the time.

  // check to see if it's time to blink the LED; that is, if the difference
  // between the current time and last time you blinked the LED is bigger than
  // the interval at which you want to blink the LED.
  unsigned long currentMillis = millis();

  if (currentMillis - previousMillis >= interval) {
    // save the last time you blinked the LED
    previousMillis = currentMillis;

    // if the LED is off turn it on and vice-versa:
    if (ledState == LOW) {
      ledState = HIGH;
    } else {
      ledState = LOW;
    }

    // set the LED with the ledState of the variable:
    digitalWrite(ledPin, ledState);
  }
}
```

Source : [https://docs.arduino.cc/built-in-examples/digital/BlinkWithoutDelay](https://docs.arduino.cc/built-in-examples/digital/BlinkWithoutDelay){target=_blank}

Cette technique à l'avantage de ne pas retarder les autres traitements et on pourrait même s'en servir pour lancer des plusieurs traitements à des intervalles différents. 
