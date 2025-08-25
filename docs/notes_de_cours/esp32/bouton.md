# Boutons

Le bouton est un petit dispositif physique qui va permettre au courant de passer ou non. Quand le bouton est appuyé, le circuit interne est fermé et le courant passe. Il nous est possible de "lire" par une broche si le courant passe ou non et d'exécuter du code en conséquence.

Les boutons avec lesquels nous allons travailler sont composés de 4 broches disposées par deux sur deux côtés opposés. Les broches du bouton sont reliées entre elles de la façon suivante: en plaçant le bouton face contre nous, un des côtés avec des broches vers le haut, les broches de gauche sont reliées entre elles et celles de droite aussi.

![button_01](\assets\images\button_01.png){.center .shadow}

## Branchement du bouton

Quand le bouton est relâché, il est dans un état indéterminé ("flottant") qui ne correspond pas nécessairement à l'état réel du bouton. Pour palier à ce problème on va utiliser une connexion au neutre ("LOW") ou à la source de tension ("HIGH") via une résistance. La connexion stabilise la lecture sur la broche quand le bouton est relâché.  

Un tel circuit est appelé "PULL-DOWN" quand la connexion est faite avec le neutre ("LOW") quand le bouton est relâché et "PULL-UP" quand la connexion est vers la source de tension ("HIGH") 
 
On peut utiliser un circuit interne du ESP32 pour les PULL-DOWN/PULL-UP ou bien utiliser un circuit externe avec résistance physique.

### Cicuit interne

Pour relier un bouton en utilisant la résistance interne on va brancher une broche du haut a un port GPIO et une broche du bas en diagonale à la mise à la terre.  La broche va être connectée directement au neutre quand le bouton est appuyé (lecture de "LOW")

![button_02](\assets\images\button_02.png){.center}

![button_03](\assets\images\button_03.png){.center}

Ensuite dans le code on va encore s'initialiser une constante avec le numéro du GPIO où le bouton est branché. 

`#define PIN_BUTTON 8`

Dans la fonction setup() on va initialiser la broche avec pinMode à INPUT_PULLUP pour indiquer qu'on utilise le circuit interne qui va indiquer HIGH quand le bouton est relâché.

`pinMode(PIN_BUTTON, INPUT_PULLUP);`

La fonction digitalRead() va nous retourner un byte : 0 (LOW) ou 1 (HIGH).

``````c
byte etatBouton = digitalRead(PIN_BUTTON);
if (etatBouton == LOW) {
    // Broche relié au neutre:  bouton appuyé
    // ...
}
``````

## À vous de jouer

- [x] Créez le montage affiché plus haut et écrivez un sketch qui va écrire à la console en continu si le bouton est pressé ou non.
- [x] Est-ce que vous remarquez quelque chose de particulier? Est-ce que le texte affiché est toujours correct.
- [x] Faites une petite recherche sur le phénomène de "Debounce" et ajustez votre code pour pallier à ce problème.



