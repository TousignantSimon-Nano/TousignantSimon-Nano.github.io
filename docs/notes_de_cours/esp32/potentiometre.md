# Le potentiomètre

Le potentiomètre est un capteur qui permet d'appliquer une résistance variable sur une broche et en conséquence une lecture de tension qui varie continuellement avec la position du contrôle. La valeur sera déterminée par selon un angle compris entre 0 (du côté du *ground*) et 275 degrées.

## Branchement

Le capteur comprends trois broches. Si on met le potientomètre à plat, avec le "bras" orienté vers le haut et les broches tournées vers nous, les branchements sont les suivants : 

- À gauche : La mise à la terre
- Au milieu : La sortie qu'on connecte à un GPIO du ESP32
- À droite : L'alimentation 3.3V

![pot_01.png](\assets\images\pot_01.png){.center}

## Comment lire sa valeur

On doit faire une lecture analogue de la broche GPIO sur laquelle on a connecté le potentiomètre. 

```c linenums="1"
#define BROCHE_POTENT 4
pinMode(BROCHE_POTENT, INPUT);
int valeur = analogRead(BROCHE_POTENT);
```

La valeur lue sera calculée par le esp32 selon l'angle du potentiomètre et le voltage résultant. L'échantillonneur (sampler) du ESP32 a un résolution de 12 bit, donc la valeur lue sera située entre 0 et 4095 (2^12^). On peut facilement convertir la valeur selon un autre échelle avec la foncion `map()`. 

```c
map(valeur, minOrigine, maxOrigine, minDest, maxDest);
```

- valeur : La valeur à convertir
- minOrigine : La valeur minimum de l'échelle d'origine
- maxOrigine : La valeur maximum de l'échelle d'origine
- minDest : La valeur minimum de l'échelle de destination
- maxDest : La valeur maximum de l'échelle de destination

Dans l'exemple suivant la valeur passera d'une valeur entre 0 et 4095 à une valeur entre 0 et 100

```c title="Exemple map()" linenums="1"
pinMode(4, INPUT);
int valeur = analogRead(4);
int valeurMap = map(valeur, 0, 4095, 0, 100);
```

## À vous de jouer

- [x] Créez le montage affiché plus haut et écrivez un sketch qui va écrire à la console avec un intervalle de 500ms la valeur du potentiomêtre.
- [x] Ajoutez une DEL à votre montage et trouvez une façon de faire varier son intensité selon la valeur du potentiomêtre. 
