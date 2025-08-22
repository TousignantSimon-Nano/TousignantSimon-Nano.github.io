# DEL

Une diode électroluminescente (DEL) est un petit dispositif qui peut émettre de la lumière quand on lui applique un courant électrique. La DEL comporte deux branches, l'une plus longue que l'autre, et le sens de branchement est important. La plus longue branche correspond au positif (+) et doit être branché sur la sortie positive de l'alimentation. À l'inverse la branche courte est le négatif (-) et doit être reliée à la mise à la terre (ground).

![del_01](\assets\images\del_01.png){.center .shadow}

## Petit calcul et résistance

La DEL doit être traverser par le bon voltage de courant qui se situe généralement entre 1.9 et 3.4 volts selon le modèle. On doit aussi ajouter une résistance à la DEL pour la protéger d'une trop grande consomation de courant. La DEL à donc une intensité de courant maximale à ne pas dépasser.

!!! danger

    Ne brancher jamais une DEL directement à la source de courant, vous allez la brûler.

Dans notre kit ESP32 nous avons 4 couleurs de DEL différentes. Prenez notes que le voltage et l'intensité de courant varient selon la couleur de la DEL 

| Couleur | Voltage | Courant maximal |
| ------- | ------- | --------------- |
| Rouge   | 2V      | 20mA            |
| Jaune   | 2.1V    | 20mA            |
| Verte   | 2.2V    | 10mA            |
| Bleu    | 3.3V    | 10mA            | 

![del_04](\assets\images\del_04.png){.center .shadow}

La résistance à appliquer, exprimer en Ohm (Ω), va donc varier selon la couleur de la DEL et de la source de courant qu'on va utiliser. On peut utiliser la [loi de Ohm](https://www.fluke.com/en-us/learn/blog/electrical/what-is-ohms-law){target=_blank} pour calculer la résistance qu'on peut résumer par le calcul suivant : 

`(Voltage de ma source de courant - voltage maximal de ma DEL) / Courant maximal en ampère`

N'oubliez pas que les valeurs du tableau sont en mA et qu'il faut les diviser par 1000 pour les ramener en ampères. Vous êtes maintenant capable de mesurer la résistance requise pour une DEL, je vous donne le droit d'utiliser un calculateur en ligne : [https://www.circuitbread.com/toolbox/led-resistor-calculator](https://www.circuitbread.com/toolbox/led-resistor-calculator){target=_blank}

### La résistance

Une résistance est un équipement électronique passif qui limite et régularise le débit du courant dans un circuit électronique. Il n'y a pas de borne positive ou négative sur une résistance, on peut la brancher dans un sens ou dans l'autre. Par contre il y a une série de ligne de couleur qui nous indique la valeur de la résistance. Pour apprendre à déchiffrer ce code de couleur, je vous invite à consulter l'article suivant : [https://www.positron-libre.com/cours/electronique/resistances/code-couleurs-resistances.php](https://www.positron-libre.com/cours/electronique/resistances/code-couleurs-resistances.php){target=_blank}.

![del_02](\assets\images\del_02.png){.center .shadow}

## Branchement sur la planche de maquettage

La planche de maquettage (Breadboard) est litéralement une petite planche muni de trou dans lesquelles ont peut brancher nos composants sans nécessiter de soudure, pratique pour l'expérimentation. Les trous sont relié entre eux et forme de petits circuits de la façon suivante : 

![del_02](\assets\images\del_03.png){.center .shadow}

De chaque côté vous avez aussi une ligne rouge et bleu qui correspont à un circuit d'alimentation positive (rouge) et négative (bleu).

!!! important

    Débrancher toujours l'alimentation de votre ESP32 pendant que vous faites votre montage

On va maintenant faire un branchement simple d'une DEL rouge à notre ESP32. Le schéma est pour le modèle avec la carte d'extension. Vous pouvez très bien l'adapter pour le brancher directement au ESP32. Pour ce montage vous avez besoin de : 

- Un DEL rouge
- Une résistance de 220 ohms
- Deux cables de racordement

<figure markdown>
  ![del_05](\assets\images\del_05.png){.center .shadow}
  <figcaption>Promis les prochains montage je fais des schémas plus jolie</figcaption>
</figure>

## Faisons clignoter la DEL

On va reprendre le premier sketch qu'on avait fait pour faire clignoter la DEL incluse sur le ESP32. Vous l'avez deviné on va faire clignoter notre belle DEL rouge. Comme on peut voir sur le schéma j'ai branché le circuit qui alimente la DEL sur le GPIO2.

``````c linenums="1"
// On stocke dans une constante le numéro du GPIO utilisé
#define PIN_DEL 2

void setup() {
  // On initialize la pin en sortie
  pinMode(PIN_DEL, OUTPUT);
}

void loop() {
  // Allume la DEL
  digitalWrite(PIN_DEL, HIGH);
  delay(1000);
  // Éteins la DEL
  digitalWrite(PIN_DEL, LOW);
  delay(1000);
}
``````

- [x] Testez votre branchement avec cet extrait de code, votre DEL devrait allumer. Vous avez surement remarqué que la DEL du ESP32 s'est mise à clignoter elle aussi. C'est parce qu'elle est également branché au GPIO2.
- [x] Changez votre branchement pour utiliser un autre port GPIO. Vous pouvez vous référer au schéma de la page sur les broches du ESP32. Vous pouvez utiliser n'importe quel broche GPIO Entrée et sortie (Input and Output). Ajuster votre code selon votre nouveau branchement.

