# 🐚 Bash Cheat Sheet

Un aide-mémoire des commandes et concepts essentiels en Bash.

---

## 🔹 Navigation
- `pwd` – afficher le répertoire courant  
- `ls` – lister les fichiers  
  - `ls -l` (détails)  
  - `ls -a` (inclure fichiers cachés)  
- `cd <dossier>` – changer de répertoire  
  - `cd ..` – remonter d’un niveau  
  - `cd ~` – aller au répertoire utilisateur  

---

## 🔹 Fichiers & dossiers
- `touch fichier.txt` – créer un fichier vide  
- `mkdir dossier` – créer un dossier  
- `cp source dest` – copier fichier/dossier  
- `mv source dest` – déplacer/renommer  
- `rm fichier` – supprimer un fichier  
  - `rm -r dossier` – supprimer un dossier récursivement  

---

## 🔹 Affichage & lecture
- `cat fichier.txt` – afficher contenu  
- `less fichier.txt` – parcourir contenu (page par page)  
- `head -n 10 fichier.txt` – premières lignes  
- `tail -n 10 fichier.txt` – dernières lignes  
- `tail -f log.txt` – suivre un fichier en direct  

---

## 🔹 Redirections & pipes
- `commande > out.txt` – rediriger sortie standard  
- `commande >> out.txt` – ajouter à la fin du fichier  
- `commande < in.txt` – utiliser fichier comme entrée  
- `commande1 | commande2` – envoyer sortie de 1 dans entrée de 2  

---

## 🔹 Permissions
- `chmod 755 fichier` – changer permissions  
- `chown user:group fichier` – changer propriétaire  
- `ls -l` – voir permissions (ex : `-rw-r--r--`)  

---

## 🔹 Processus
- `ps` – voir processus en cours  
- `top` – vue interactive (CPU, mémoire)  
- `kill <PID>` – tuer un processus  
- `&` – exécuter en arrière-plan (`commande &`)  
- `jobs` – lister les jobs en arrière-plan  
- `fg %1` – ramener un job au premier plan  

---

## 🔹 Recherche
- `grep "mot" fichier.txt` – rechercher texte  
- `grep -r "mot" dossier/` – recherche récursive  
- `find . -name "*.txt"` – trouver fichiers par nom  

---

## 🔹 Réseau
- `ping site.com` – tester la connexion  
- `curl http://site.com` – requête HTTP simple  
- `wget URL` – télécharger un fichier  

---

## 🔹 Variables & scripts
- `VAR="hello"` – définir une variable  
- `echo $VAR` – afficher une variable  
- `export VAR="valeur"` – variable globale  
- `./script.sh` – exécuter un script  
- `bash script.sh` – exécuter avec Bash  

---

## 🔹 Astuces pratiques
- `history` – afficher l’historique des commandes  
- `!!` – rejouer la dernière commande  
- `!n` – exécuter la commande numéro *n* du `history`  
- `CTRL + R` – recherche dans l’historique interactif  
- `alias ll="ls -lah"` – créer un raccourci de commande  

---