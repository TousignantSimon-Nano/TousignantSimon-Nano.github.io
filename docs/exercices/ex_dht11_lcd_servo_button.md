# Exercice - Station Météo Interactive avec LCD, Servo et DHT11

Cet exercice combine plusieurs composants et concepts pour créer une station météo interactive, contrôlée via des interactions physiques (bouton) et série (commandes).

## Objectifs d'apprentissage :
- Utilisation du capteur DHT11 pour la température et l'humidité.
- Affichage de données sur un écran LCD via un module I2C.
- Contrôle d'un servomoteur pour une représentation visuelle analogique.
- Gestion d'un bouton-poussoir pour des actions interactives.
- Implémentation d'interruptions et utilisation du mot-clé `volatile`.
- Communication série bidirectionnelle avec l'Arduino.

## Matériel Requis :
- Arduino UNO (ou compatible)
- Capteur de température et d'humidité DHT11 (le modèle bleu)
- Module LCD 16x02 avec interface I2C
- Servomoteur 3 fils (standard SG90 ou similaire)
- Bouton-poussoir
- Résistance 10kΩ (si le DHT11 n'a pas de pull-up intégré)
- Planche à prototyper (breadboard), fils de connexion
- Source d'alimentation externe pour le servomoteur (si nécessaire, ex: 4x AA batteries ou un pack batterie 5V)
- Un morceau de carton ou de papier pour créer une "aiguille" pour le servomoteur.

## Montage (Schémas Génériques) :
Référez-vous aux notes de cours des semaines précédentes pour les schémas de branchement spécifiques :
- **LCD I2C** : Connectez VCC, GND, SDA (A4 sur UNO) et SCL (A5 sur UNO) à l'Arduino.
- **DHT11** : Connectez VCC, GND, et la broche Data (à une broche numérique, ex: D2). Assurez-vous d'avoir une résistance de pull-up de 10kΩ entre VCC et Data si votre module n'en a pas.
- **Servomoteur** : Connectez le fil de signal (Orange/Jaune) à une broche PWM de l'Arduino (ex: D9). Connectez le VCC (Rouge) et le GND (Marron/Noir) du servomoteur à une **alimentation externe**. N'oubliez pas de connecter le **GND de l'alimentation externe au GND de l'Arduino** !
- **Bouton-poussoir** : Connectez une patte à GND et l'autre à une broche numérique d'interruption (ex: D3) configurée en `INPUT_PULLUP` (ou avec une résistance de pull-up externe).

## Instructions Détaillées :

### 1. Affichage LCD : Température & Humidité
- L'écran LCD 16x02 doit afficher la température et l'humidité.
- **Ligne 1 :** Affichera la température. Initialement en Celsius, mais pourra basculer en Fahrenheit via un bouton.
- **Ligne 2 :** Affichera toujours l'humidité relative en pourcentage.
- Exemple de format : `Temp: 25.0 C` et `Hum : 60.5 %`

### 2. Servomoteur - Jauge d'Humidité
- Le servomoteur doit être utilisé comme une "aiguille" analogique.
- Le mouvement du servomoteur doit être "mappé" sur la plage de 0% à 100% d'humidité.
  - 0% d'humidité -> position minimale du servo (ex: 0 degrés)
  - 100% d'humidité -> position maximale du servo (ex: 180 degrés)
- Fixez une petite aiguille en papier au servomoteur pour visualiser le mouvement.

### 3. Bouton-poussoir - Contrôle Interactif
- Connectez un bouton-poussoir à une broche d'interruption de l'Arduino UNO (Broche 2 ou 3).
- **Lors d'un appui (FALLING edge) :**
    1.  Inverse l'état du **rétroéclairage de l'écran LCD (ON/OFF)**.
    2.  Bascule l'affichage de la température de la première ligne entre **Celsius et Fahrenheit**.
- L'étudiant devra utiliser une **interruption externe** pour ce bouton et le mot-clé `volatile` pour gérer les variables partagées avec l'ISR.

### 4. Console Série - Débogage & État
- Configurez la communication série à **9600 bauds**.
- Affichez sur la console série, toutes les 2 secondes environ :
    - La température en Celsius.
    - La température en Fahrenheit.
    - L'humidité relative en pourcentage.
    - L'état actuel du rétroéclairage LCD (`ON` ou `OFF`).
    - L'unité de température affichée en première ligne de l'LCD (`Celsius` ou `Fahrenheit`).
- Exemple : `Temp C: 25.0, Temp F: 77.0, Hum: 60.5%, LCD: ON, Affiche: Celsius`

### 5. Commandes Série - Mode d'Affichage
- L'Arduino doit écouter des commandes spécifiques via le port série.
- Si la commande "C" est reçue (suivie d'un retour à la ligne), l'affichage de la première ligne de l'LCD doit basculer de façon permanente en Celsius.
- Si la commande "F" est reçue (suivie d'un retour à la ligne), l'affichage de la première ligne de l'LCD doit basculer de façon permanente en Fahrenheit.
- Si une commande "TOGGLE" est reçue, l'affichage de la première ligne de l'LCD doit basculer entre Celsius et Fahrenheit.
- Si une commande "BACKLIGHT" est reçue, le rétroéclairage de l'écran LCD doit basculer (ON/OFF).
- L'étudiant devra utiliser la méthode `SerialEvent()` pour gérer ces commandes de manière non bloquante.

## Étapes de Réalisation (Suggestion) :

1.  **Mise en place des librairies :** Installez `LiquidCrystal_I2C`, `Servo`, et `DHT sensor library`.
2.  **Branchements :** Réalisez le montage de tous les composants en vous basant sur les notes de cours. **Attention à l'alimentation du servomoteur et à la masse commune !**
3.  **Code de base DHT11 :** Commencez par lire et afficher les données du DHT11 sur le moniteur série.
4.  **Code LCD :** Intégrez l'écran LCD pour afficher la température et l'humidité.
5.  **Code Servomoteur :** Ajoutez le contrôle du servomoteur pour l'humidité. Utilisez la fonction `map()`.
6.  **Code Bouton (Interruption) :** Implémentez l'interruption pour le bouton, en gérant le `volatile` pour les variables partagées (rétroéclairage et unité de température LCD).
7.  **Code Commandes Série :** Implémentez `SerialEvent()` pour les commandes "C", "F", "TOGGLE" et "BACKLIGHT".
8.  **Affichage Série Complet :** Finalisez l'affichage sur la console série avec toutes les informations requises.

## À Remettre :
- Le schéma de votre montage final (dessin à la main ou logiciel de CAO).
- Le code Arduino (.ino) complet et commenté.
- Une courte vidéo de démonstration du fonctionnement de votre station météo.
