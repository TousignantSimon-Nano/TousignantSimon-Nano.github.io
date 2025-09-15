# Théorie : La variable PATH en Linux

## 1. Qu’est-ce que la variable PATH ?
La variable d’environnement `PATH` contient une liste de **répertoires** dans lesquels le shell va chercher les **commandes exécutables** que vous tapez dans le terminal.

- Exemple : lorsque vous tapez `ls`, le shell cherche l’exécutable `ls` dans chacun des répertoires listés dans `PATH`.
- Si le répertoire n’est pas dans `PATH`, vous devez indiquer le **chemin complet** pour exécuter le programme.

---

## 2. Vérifier la valeur de PATH
Pour afficher la valeur actuelle de `PATH` :
```bash
echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/utilisateur/mes_scripts
```

##3. Ajouter un répertoire à PATH

Pour pouvoir exécuter vos scripts depuis n’importe quel répertoire, ajoutez le dossier contenant vos scripts à PATH :

###Temporaire (pour la session en cours)

```bash
export PATH=$PATH:/home/utilisateur/mes_scripts
# attention le =$PATH est important c'est comme si on faisait un += en c#
```

###Permanent (à chaque ouverture du terminal)

Ajouter la ligne précédente dans ~/.bashrc :
```bash
# on fait une écriture en ajout ">>" dans le fichier .bashrc dans le dossier de l'utilisateur courant. On peut le faire aussi avec nano
echo 'export PATH=$PATH:/home/utilisateur/mes_scripts' >> ~/.bashrc
  
# on recharge la configuration du fichier .bashrc manuellement. Le fichier .bashrc est exécuté à chaque ouverture de session.
source ~/.bashrc
```