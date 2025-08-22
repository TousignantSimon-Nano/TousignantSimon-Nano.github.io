# Exercice 09 - Le jeu Simon

Dans cet exercice on va reproduire le jeu Simon avec notre ESP32. Si vous ne connaissez pas le jeu, vous en avez un aperçu ici : [https://fr.wikipedia.org/wiki/Simon_(jeu)](https://fr.wikipedia.org/wiki/Simon_(jeu)){target=_blank}

On va simplifier le montage en n'utilisant que deux couleurs pour notre jeu: jaune et bleu  

## Principe du jeu

Le jeu consiste à reproduire une suite de couleur générée aléatoirement. La suite commence par une seule couleur et un nouvel élément s'ajoute à chaque fois que le joueur réussi à reproduire la suite. Exemple : 

- Premier round : jaune. 
- Deuxième round : jaune, jaune
- Troisième round : jaune, jaune, bleu
- Etc.

Le but du jeu est d'atteindre le round le plus élevé. Le jeu se termine quand on atteint le niveau 10.

## Montage

Pour notre jeu, nous allons faire un montage avec : 

- Un écran LCD
- Une DEL jaune et une DEL bleu
- Un bouton jaune et un bouton bleu
- Un *buzzer* passif

!!! Attention

        Vous devez tenir compte de l'effet de *debounce* sur vos boutons.
        Utilisez la fonction *outputCW* de la librairie *DacESP32* pour vous assurez que votre code répond toujours lors de la génération de sons. 

## Déroulement du jeu

### Écran de démarrage

- Au démarrage, sur l'écran LCD on affiche sur la première ligne "Simon le jeu" et "Meilleur: xxx" sur la deuxième ligne où xxx représente le meilleur niveau atteint par les joueurs. (Le record se réinitialise à chaque démarrage)
- Le jeu va commencer si on appuie sur un des deux boutons.

### Écran niveau

- Pour chaque niveau:
    - Affiche "Niveau x" sur la première ligne et "Mémorise" sur la deuxième (x représente le niveau actuel)
    - Reproduit la suite sur les DEL pendant 1 seconde par élément.
    - Un son associé a chaque couleur est joué en meme temps que la DEL s`allume.
    - Ensuite affiche "Niveau x" sur la première ligne et "Votre tour" sur la deuxième ligne + un son plus aigu est joué
    - Il n'y a pas de limite de temps pour le joueur
    - Le joueur doit reproduire la suite avec les boutons aux couleurs correspondantes
    - La DEL et le son correspondant sont actifs lorsque le joueur appuie sur un bouton
- Si le joueur se trompe dans la suite
    - Affiche ""Niveau x" sur la première ligne et "Erreur" sur la deuxième
    - Un son plus grave est joué pour indiquer l`erreur
    - Après 5 secondes affiche *Partie terminée* sur la deuxième ligne
    - Après 5 secondes affiche l'écran de démarrage.
- Si le joueur réussit
    - Affiche "Niveau x" sur la première ligne et "Bravo" sur la deuxième
    - Une séquence de 2 sons (grave puis aigu) indique le succès 
    - Après 5 secondes affiche un nouveau niveau

   
> Optionnel: Ajouter un bouton rouge et une DEL rouge pour rendre le jeu plus intéressant
 


