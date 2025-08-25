# Exercice 05 - Sense Hat - Afficher les données 

À l'aide des capteurs de température, de pression et d'humidité, faites afficher dans des écrans séparés les valeurs de chacun.

## Écran température

- Sur les deux premières colonnes de LEDs, affichez une jauge qui sera remplie en fonction de la température. Si la température est au minimum de ce qui peut être capté, la jauge est vide. Si on est au maximum les 8 points des 2 premières colonnes sont remplis. Entre les deux ça sera un ratio.
- Dans l'espace restant sur la matrice de DELs, affichez la lettre T pour Température.
- Si on clique sur le joystick, affichez le texte : "Température 12 C" où 12 est la valeur saisie. Revenez ensuite à l'affichage de l'écran.

## Écran humidité et pression

- Pour ces deux écrans, afficher la lettre H ou P tout simplement.
- Si on clique sur le joystick, affichez le texte : "Humidité" ou "Pression" suivi de la valeur saisie. Revenez ensuite à l'affichage de l'écran.

## Navigation entre les écrans

- Les touches gauche et droite nous font passer d'un écran à l'autre.
- L'ordre des écrans est "Température" - "Humidité" - "Pression"
- Si on est sur pression et qu'on entre droite, on revient à température. La même chose dans l'autre sens.
- Chaque écran doit avoir une couleur de caractère différente.
