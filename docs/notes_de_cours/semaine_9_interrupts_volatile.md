# Arduino : Interruptions et Volatile

Cette semaine, nous allons explorer les interruptions et la notion de `volatile`, des concepts essentiels pour gérer les événements en temps réel et optimiser la réactivité de vos programmes Arduino.

---

## 1. Interruptions Série avec `Serial.read()` (Toggle LED)

Les interruptions sont des mécanismes qui permettent au microcontrôleur de suspendre son exécution normale pour traiter un événement urgent. Pour la communication série, cela signifie que vous pouvez réagir immédiatement à la réception de données sans avoir à vérifier constamment le port série dans votre `loop()`.

### La méthode `SerialEvent()`

L'IDE Arduino propose une fonction spéciale, `SerialEvent()`, qui est appelée automatiquement après chaque `loop()` si des données sont disponibles dans le buffer série. Bien que ce ne soit pas une "vraie" interruption matérielle au sens strict, elle fonctionne comme une interruption logicielle et est très utile pour gérer les communications série de manière non bloquante.

**Fonctionnement :**
- `SerialEvent()` est déclarée sans paramètre ni type de retour (`void SerialEvent()`).
- Le code à l'intérieur de `SerialEvent()` est exécuté dès que des données série arrivent, mais seulement après la fin de la fonction `loop()`.

**Exemple complet : Contrôle d'une LED par commandes série ("ON" / "OFF")**
```cpp
// Définition de la broche de la LED
const byte LED_PIN = 13; // Utilisation de la LED intégrée sur la plupart des cartes Arduino

// Variable pour stocker l'état de la LED
// Bien que non volatile pour SerialEvent car le compilateur comprend que la LED est contrôlée par digitalWrite
// et les données série sont gérées dans un contexte plus "main loop friendly",
// nous laissons la LED gérée par le code principal pour cet exemple.
byte ledState = LOW; 

// Variable pour stocker les données reçues via le port série
String receivedCommand = "";

void setup() {
  // Initialise la communication série à 9600 bauds
  Serial.begin(9600);
  // Configure la broche de la LED comme une sortie
  pinMode(LED_PIN, OUTPUT);

  Serial.println("Arduino est prêt. Envoyez 'ON' ou 'OFF' par le moniteur série.");
  Serial.println("La commande doit être suivie d'un retour à la ligne (\\n).");
}

void loop() {
  // Le code principal continue de s'exécuter ici.
  // La LED est allumée ou éteinte en fonction de 'ledState'.
  digitalWrite(LED_PIN, ledState);
  
  // Vous pouvez ajouter d'autres tâches non bloquantes ici,
  // comme lire d'autres capteurs, faire clignoter une autre LED, etc.
  // delay(100); // Pour éviter une boucle trop rapide si aucune autre tâche
}

// Cette fonction est appelée automatiquement par l'IDE Arduino après chaque appel à loop()
// si des données sont disponibles dans le buffer série.
void serialEvent() {
  while (Serial.available()) {
    // Lit le prochain caractère disponible
    char inChar = (char)Serial.read();
    // Ajoute le caractère à la chaîne de commande reçue
    receivedCommand += inChar;

    // Si un caractère de fin de ligne ('\n') est reçu, cela signifie que la commande est complète
    if (inChar == '\n') {
      // Nettoie la chaîne en retirant les caractères d'espacement (espace, \r, \n)
      receivedCommand.trim();

      Serial.print("Commande reçue: '");
      Serial.print(receivedCommand);
      Serial.println("'");

      // Traite la commande reçue
      if (receivedCommand.equalsIgnoreCase("ON")) {
        ledState = HIGH; // Allume la LED
        Serial.println("LED est ON.");
      } else if (receivedCommand.equalsIgnoreCase("OFF")) {
        ledState = LOW;  // Éteint la LED
        Serial.println("LED est OFF.");
      } else {
        Serial.println("Commande invalide. Utilisez 'ON' ou 'OFF'.");
      }
      // Réinitialise la chaîne de commande pour la prochaine réception
      receivedCommand = ""; 
    }
  }
}
```
Dans cet exemple, la `loop()` n'est pas bloquée par l'attente de données série. `SerialEvent()` gère la réception en arrière-plan (entre deux exécutions de `loop()`), permettant au programme principal de rester réactif.

---

## 2. Interruptions sur Broches Digitales (Arduino UNO) (Toggle LED)

Les interruptions externes permettent de détecter un changement d'état sur une broche numérique et d'exécuter une fonction spécifique (ISR - Interrupt Service Routine) immédiatement. Cela est crucial pour les événements sensibles au temps, comme la lecture d'un encodeur rotatif ou un bouton-poussoir.

### Broches d'interruption sur Arduino UNO

Sur l'Arduino UNO (basé sur l'ATmega328P), seules certaines broches peuvent être utilisées comme interruptions externes :
- **Broche 2 (Interrupt 0)**
- **Broche 3 (Interrupt 1)**

Ces broches sont appelées "broches d'interruption" ou "interrupt pins".

### La fonction `attachInterrupt()`

Pour configurer une interruption externe, on utilise la fonction `attachInterrupt()` :

**Syntaxe :**
```cpp
attachInterrupt(digitalPinToInterrupt(pin), ISR, mode);
```
- `digitalPinToInterrupt(pin)` : Convertit le numéro de broche Arduino en numéro d'interruption. Pour l'UNO, `digitalPinToInterrupt(2)` est 0, et `digitalPinToInterrupt(3)` est 1.
- `ISR` : La fonction de service d'interruption à exécuter lorsque l'événement se produit. Cette fonction ne doit pas prendre de paramètres et ne doit pas retourner de valeur (`void`).
- `mode` : Définit quand l'interruption doit être déclenchée :
    - `LOW` : Quand la broche est à l'état BAS.
    - `CHANGE` : Quand la broche change d'état (de BAS à HAUT, ou de HAUT à BAS).
    - `RISING` : Quand la broche passe de BAS à HAUT.
    - `FALLING` : Quand la broche passe de HAUT à BAS.

**Exemple complet : Contrôle d'une LED par un bouton-poussoir (Digital Pin Interrupt)**
```cpp
// Définition de la broche de la LED (LED intégrée sur la plupart des cartes Arduino)
const byte LED_PIN = 13; 
// Définition de la broche du bouton (doit être une broche d'interruption sur l'UNO)
const byte BUTTON_PIN = 2; // Broche 2 correspond à Interrupt 0 sur Arduino UNO

// Variable partagée entre le code principal (loop) et l'ISR.
// Doit être déclarée 'volatile' pour garantir que le compilateur ne l'optimise pas
// et que sa valeur est toujours relue de la mémoire.
volatile byte ledState = LOW; // État initial de la LED: éteinte

void setup() {
  // Configure la broche de la LED comme une sortie
  pinMode(LED_PIN, OUTPUT);
  // Configure la broche du bouton comme une entrée avec une résistance de pull-up interne.
  // Cela garantit que la broche est HIGH quand le bouton n'est pas appuyé.
  pinMode(BUTTON_PIN, INPUT_PULLUP); 

  // Initialise la communication série pour le débogage
  Serial.begin(9600);
  Serial.println("Appuyez sur le bouton connecté à la broche 2 pour allumer/éteindre la LED.");

  // Attache l'interruption à la broche du bouton.
  // digitalPinToInterrupt(BUTTON_PIN) convertit le numéro de broche (2) en numéro d'interruption (0).
  // toggleLED est la fonction de service d'interruption (ISR) qui sera appelée.
  // FALLING signifie que l'ISR sera déclenchée lorsque la broche passe de HIGH à LOW (bouton appuyé).
  attachInterrupt(digitalPinToInterrupt(BUTTON_PIN), toggleLED, FALLING); 
}

void loop() {
  // Le code principal s'exécute ici.
  // Il met à jour l'état de la LED en fonction de la variable 'ledState'
  // qui est modifiée par l'ISR.
  digitalWrite(LED_PIN, ledState);
  
  // D'autres tâches non sensibles au temps peuvent être exécutées ici.
  // Par exemple, lire des capteurs, gérer d'autres sorties, etc.
}

// Fonction de service d'interruption (ISR) pour le bouton.
// Elle est appelée lorsque le bouton est appuyé (FALLING edge).
void toggleLED() {
  // Inverse l'état de la LED (HIGH devient LOW, LOW devient HIGH).
  ledState = !ledState; 
}
```

**Règles pour les ISR :**
- **Doivent être courtes et rapides** : Le code à l'intérieur d'une ISR bloque d'autres interruptions (sauf les plus prioritaires).
- **Pas de `delay()`** : La fonction `delay()` ne fonctionne pas dans une ISR.
- **Pas de `Serial.print()`** : La communication série utilise des interruptions et pourrait causer des conflits. Si vous avez absolument besoin de déboguer à partir d'une ISR, vous pouvez définir un drapeau `volatile` et l'imprimer dans la `loop()`.
- **Les variables partagées avec la `loop()` doivent être `volatile`** (voir section suivante).

---

## 3. La Notion de `volatile` pour les Interruptions

Lorsqu'une variable est utilisée à la fois dans la fonction `loop()` (ou n'importe quelle partie du code principal) et dans une fonction de service d'interruption (ISR), il est crucial de la déclarer avec le mot-clé `volatile`.

### Pourquoi `volatile` ?

Les compilateurs C++ effectuent des optimisations pour rendre le code plus rapide et plus compact. Si une variable n'est pas modifiée explicitement dans la `loop()`, le compilateur peut supposer que sa valeur ne change pas et décider de la stocker dans un registre interne du microcontrôleur ou de ne pas la relire de la mémoire à chaque fois.

Or, une ISR peut modifier cette variable à tout moment, indépendamment de la `loop()`. Sans `volatile`, la `loop()` pourrait continuer à utiliser une copie obsolète de la variable (celle qui était dans le registre), conduisant à un comportement inattendu et à des bugs difficiles à diagnostiquer.

Le mot-clé `volatile` indique au compilateur que la variable peut être modifiée à tout moment par des événements externes (comme une interruption) et qu'il doit toujours la relire directement de la mémoire à chaque fois qu'elle est accédée, sans aucune optimisation qui pourrait empêcher cela.

**Exemple : `volatile` dans l'exemple du bouton**
```cpp
// ...
volatile byte ledState = LOW; // ledState est partagée entre loop() et toggleLED()
// ...
```
Dans cet exemple, `ledState` est déclarée `volatile` car `loop()` la lit (`digitalWrite(LED_PIN, ledState);`) et `toggleLED()` (l'ISR) la modifie (`ledState = !ledState;`).

### Utilisation pratique :

- Déclarez toujours `volatile` toute variable qui est lue ou écrite par une ISR ET par le code principal.
- Les types de données pour les variables `volatile` devraient être des types atomiques (byte, int, long) et si possible de 8 bits ou 16 bits pour les microcontrôleurs 8 bits comme l'UNO, afin d'éviter les problèmes de lecture/écriture multi-octets non atomiques qui pourraient être corrompus par une interruption.
