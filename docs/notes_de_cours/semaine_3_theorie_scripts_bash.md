# Théorie : Scripts Bash – Gestion des menus, saisies et fonctions

Tous les script commencent par la ligne :
```bash
#!/bin/bash
```

## 1. Afficher un menu
En Bash, un menu peut être affiché avec de simples `echo` :
```bash
echo "=== Menu Principal ==="
echo "1. Monter la partition"
echo "2. Démonter la partition"
echo "3. Quitter"
```

---

## 2. Lire un choix utilisateur et le mettre en variable
La commande `read` permet de récupérer une saisie :
```bash
read -p "Votre choix : " choix
```
La valeur saisie est stockée dans la variable `choix`.

---

## 3. Afficher un message d’utilisation si le choix est invalide
Une structure conditionnelle (`case` ou `if`) permet de gérer les choix :
```bash
case "$choix" in
  1) echo "Montage en cours..." ;;
  2) echo "Démontage en cours..." ;;
  3) echo "Au revoir !" ;;
  *) echo "Erreur : choix invalide. Veuillez entrer 1, 2 ou 3." ;;
esac
```

---

## 4. Boucle "tant que le choix est invalide"
On peut utiliser `while` pour répéter la demande tant que l’entrée n’est pas correcte :
```bash
choix=""
while [[ "$choix" != "1" && "$choix" != "2" && "$choix" != "3" ]]
do
  echo "=== Menu Principal ==="
  echo "1. Monter la partition"
  echo "2. Démonter la partition"
  echo "3. Quitter"
  read -p "Votre choix : " choix

  case "$choix" in
    1) echo "Montage en cours..." ;;
    2) echo "Démontage en cours..." ;;
    3) echo "Au revoir !" ;;
    *) echo "Erreur : choix invalide." ;;
  esac
done
```

---

## 5. Notion de sous-routine (fonction)
Une **fonction Bash** permet de regrouper un ensemble de commandes qu’on peut appeler plusieurs fois.

Exemple :
```bash
monter_partition() {
    echo "Montage de la partition en cours..."
    # commandes de montage ici
}

demonter_partition() {
    echo "Démontage de la partition en cours..."
    # commandes de démontage ici
}
```

Appel de la fonction depuis le menu :
```bash
case "$choix" in
  1) monter_partition ;;
  2) demonter_partition ;;
  3) echo "Au revoir !" ;;
  *) echo "Erreur : choix invalide." ;;
esac
```

---

## 6. Rendre un script exécutable et l’exécuter  

Avant de pouvoir lancer un script Bash, il faut lui donner les permissions d’exécution.

### Commande pour rendre un script exécutable  
```bash
chmod +x mon_script.sh  
```
chmod → change les permissions d’un fichier.  
  
+x → ajoute le droit d’exécution pour l’utilisateur (et éventuellement groupe/autres).  

### Exécution du script  

Une fois le script exécutable, on peut le lancer avec :
```bash
./mon_script.sh  
```
    ./ → indique que le script se trouve dans le répertoire courant.

    Sans chmod +x, le script ne pourra pas s’exécuter directement.

Exemple
```bash
nano test.sh
# écrire des commandes dans le script
chmod +x test.sh
./test.sh

```
Ce bloc permet de préparer et exécuter n’importe quel script Bash sur le Raspberry Pi.

## Résumé
- `echo` → afficher le menu.  
- `read` → saisir une valeur dans une variable.  
- `case` (ou `if`) → tester la valeur.  
- `while` → répéter la demande tant que l’entrée est invalide.  
- `function_name() { ... }` → définir une sous-routine réutilisable.  
- `function_name` → appeler la fonction.  

---

