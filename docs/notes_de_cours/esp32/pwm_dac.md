
# PWM (Pulse-Width Modulation)

- Signal de sortie binaire (0V ou 3.3V) donc le % de temps à 3.3V (*duty cycle*) est contrôlable
- Utilisé pour le contrôle de servomoteurs et autres équipements
- Peut servir à controller le niveau de luminosité d'une DEL
- Toutes les broches en sortie de l'ESP32 peuvent générer un signal PWM (broches 1 à 32)

La fonction a utiliser est *analogWrite()*. 


# DAC (Digital-to-Analog Converter)

- 2 canaux DAC (résolution 8-bit) sont disponibles sur le ESP32, via les broches 25 et 26 seulement
- Génèrent un véritable signal analogique variant de 0V à 3.3V
- Peuvent servir à controller l'intensité de DELs (ex. strips de DEL RGB), générer du son ou controller des jauges analogiques 
- 3 modes d'opération
    - Sortie directe de valeur analogique avec *dacWrite()*
    - Sortie de signal via un tableau de valeurs en mémoire 
    - Génération de signal sinusoidal d'une fréquence et amplitude donnée

Librairie Arduino à utiliser: **DacESP32**

[Plus d'info sur le site DroneBot Workshop](https://dronebotworkshop.com/esp32-dac/)



