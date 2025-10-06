# Notes sur grep, egrep et pgrep

---

## 1. grep : la base du filtrage de texte

`grep` = **Global Regular Expression Print**

### Syntaxe

```bash
grep [options] "motif" fichier
```

### Exemples

* Chercher le mot `hello` dans `fichier.txt` :

```bash
grep "hello" fichier.txt
```

* Ignorer la casse :

```bash
grep -i "hello" fichier.txt
```

* Afficher les numéros de lignes :

```bash
grep -n "hello" fichier.txt
```

* Chercher récursivement dans un dossier :

```bash
grep -r "hello" /chemin/du/dossier
```

* Exclure un motif :

```bash
grep -v "erreur" fichier.log
```

* Afficher seulement le nombre de lignes correspondantes :

```bash
grep -c "hello" fichier.txt
```

### Options utiles

* `-w` → correspond au mot entier  
```bash
grep -w "root" /etc/passwd  
```
Ne matchera que "root" comme mot complet, pas "rooter".  
* `-l` → affiche juste les noms de fichiers contenant le motif  
```bash
grep -l "error" *.log  
```
* `-E` → active les **expressions régulières étendues** (alias `egrep`)  
```bash
grep -E "chat|chien" fichier.txt  
```
Cherche "chat" ou "chien" dans le fichier.  
* `-o` → affiche seulement la partie du texte correspondant au motif
```bash
grep -o "[0-9]\+" fichier.txt   
```
Affiche uniquement les nombres trouvés dans le fichier.

### Exercices Linux

1. Chercher toutes les occurrences du mot "error" dans `/var/log/syslog`.
2. Compter le nombre de lignes contenant "root" dans `/etc/passwd`.
3. Afficher les lignes contenant "bash" mais pas "sh" dans un fichier donné.

---

## 2. egrep : grep "amélioré" pour les regex

`egrep` = **Extended GREP**

### Syntaxe

```bash
egrep "motif_regex" fichier
```

### Exemples

* Chercher `chat` ou `chien` :

```bash
egrep "chat|chien" fichier.txt
```

* Chercher une ligne qui commence par une majuscule :

```bash
egrep "^[A-Z]" fichier.txt
```

* Chercher une ligne qui se termine par un chiffre :

```bash
egrep "[0-9]$" fichier.txt
```

> ⚠️ Depuis quelques années, `egrep` est considéré comme **obsolète**, `grep -E` fait exactement la même chose.

### Exercices Linux

1. Chercher toutes les lignes dans `/var/log/auth.log` qui contiennent soit "Failed" soit "Accepted".
2. Afficher les lignes de `/etc/passwd` qui commencent par une lettre majuscule.
3. Chercher les lignes dans un fichier qui contiennent exactement 3 chiffres consécutifs.

---

## 3. pgrep : recherche de processus

`pgrep` = **Process GREP**

### Syntaxe

```bash
pgrep [options] motif
```

### Exemples

* Trouver tous les processus `ssh` :

```bash
pgrep ssh
```

* Afficher PID et nom du processus :

```bash
pgrep -l ssh
```

* Chercher un processus précis appartenant à un utilisateur :

```bash
pgrep -u alice bash
```

* Exclure certains processus avec `-v` :

```bash
pgrep -v systemd
```

* Combiner avec `kill` pour stopper un processus :

```bash
kill $(pgrep firefox)
```

* Chercher des processus et afficher leur commande complète :

```bash
pgrep -a nginx
```

### Exercices Linux

1. Lister tous les processus de l'utilisateur courant.
2. Trouver le PID du processus `cron` et l'arrêter.
3. Combiner `pgrep` et `kill` pour arrêter tous les processus `python`.

---

## Résumé rapide

| Commande | Usage principal          | Astuce                                                                          |              |
| -------- | ------------------------ | ------------------------------------------------------------------------------- | ------------ |
| grep     | Filtrer du texte         | `-i` pour ignorer la casse, `-v` pour inverser, `-o` pour partie correspondante |              |
| egrep    | grep avec regex étendues | `grep -E` remplace egrep, pratique pour `                                       | `, `+`, `()` |
| pgrep    | Chercher des processus   | `-l` pour nom + PID, `-u` pour utilisateur, `-a` pour commande complète         |              |
