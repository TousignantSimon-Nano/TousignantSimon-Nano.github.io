# Le moniteur série

On vient de voir qu'on pouvait depuis le ESP32 écrire dans le moniteur série. Mais il est aussi possible d'envoyer de l'information au ESP32 depuis le moniteur série.

## Écrire du ESP32 au pc

On intialise le port série et on indique la vitesse de transfert avec `Serial.begin(112500);`

Ensuite pour envoyer de l'informations on peut utiliser : 

- `Serial.print()` : Envoie le texte en paramètre
- `Serial.println()` : Envoie le texte en paramètre et saute une ligne
- `Serial.write()` : Envoie l'information en binaire

```c 
void setup() {
  Serial.begin(9600);
  // Affiche le texte Hello dans la console série et saute une ligne
  Serial.print("Hello ");
  Serial.println("World");
}
```

## Envoyer de l'information depuis le pc

Dans la section "Serial Monitor" de Arduino IDE il y a une section "Message" où on peut entrer notre texte.

![serial_monitor_01](\assets\images\serial_monitor_01.png){.center .shadow}

Dans le sketch, on va commencer par initialiser le port série. Ensuite dans la boucle de traitement on va vérifier s'il y a de données qui arrive du port série avec la fonction `Serial.available()` qui retourne True s'il y en a.

```c
if(Serial.available()) {
  // mon code
}
```

Il nous reste maintenant à lire les données provenant du port série. Il y a plusieurs fonctions de lecture, nous allons pour l'exemple utiliser `Serial.readStringUntil()`. Cette fonction va lire et retourner les caractères jusqu'à ce qu'elle lise un caractère qu'on lui donne en paramètre OU si un timeout est atteint. 

Le timeout par défaut est 1000ms, il peut être changé à l'aide de `Serial.setTimeout(ms)`

Lisons les charactères entrant sur le port série en utilisant le caratère `\n` (indiquant une nouvelle ligne) comme caratère de fin.  Ce caractère ne sera pas inclus dans la chaine retournée par la fonction.

```c
String monTexte = Serial.readStringUntil('\n');
```

Attention, on doit passer en paramètre un caractère et non une chaine de texte, il faut utiliser l'apostrophe (') et non le guillement (").

S'il y a des données recues sur le port série avant qu'elle ne soit lues, elles sont gardées en mémoire tampon.

## On met ça en pratique

Créer un sketch qui va nous permettre d'envoyer deux ordres au ESP32. Chaque ordre sera un mot unique de votre choix. Une des ordres sera de faire allumer la DEL et l'autre l'éteindra.

## On complique un peu les choses

Maintenant que votre sketch fonctionne, modifiez le pour utiliser d'autres fonctions de lecture du port série :

1. Faites une version qui va utiliser `Serial.read()`
2. Faites une deuxième version qui va utiliser `Serial.readBytes()`

Vous pouvez vous référez à la documentation de Arduino : [https://www.arduino.cc/reference/en/](https://www.arduino.cc/reference/en/){target=_blank}
