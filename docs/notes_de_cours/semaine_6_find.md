# Commande `find` — Recherche avancée de fichiers et répertoires

## 1. Introduction

La commande **`find`** est un outil puissant sous Linux/Unix permettant de **rechercher des fichiers et des répertoires** selon divers critères : nom, type, taille, date de modification, permissions, etc.  
Elle peut également exécuter des **actions** sur les fichiers trouvés, comme les supprimer, les copier ou modifier leurs permissions.

Sur un **Raspberry Pi**, `find` est un allié précieux pour naviguer dans les fichiers du système, repérer des scripts, des journaux ou des fichiers temporaires inutiles.

---

## 2. Syntaxe générale

```bash
find [chemin] [options] [expression]
```

### Exemples simples
- Rechercher tous les fichiers dans le répertoire courant :
  ```bash
  find . -type f
  ```

- Rechercher tous les répertoires dans `/home/robert` :
  ```bash
  find /home/robert -type d
  ```

- Rechercher un fichier par nom :
  ```bash
  find /home/robert -name "script.py"
  ```

---

## 3. Options et critères de recherche

| Option | Description |
|:-------|:-------------|
| `-name "motif"` | Recherche par nom exact ou avec joker (`*`, `?`). |
| `-iname "motif"` | Recherche insensible à la casse. |
| `-type f` | Recherche uniquement les **fichiers**. |
| `-type d` | Recherche uniquement les **répertoires**. |
| `-size +100M` | Fichiers de plus de 100 mégaoctets. |
| `-size -1M` | Fichiers de moins d’un mégaoctet. |
| `-mtime -7` | Fichiers modifiés il y a moins de 7 jours. |
| `-mtime +30` | Fichiers modifiés il y a plus de 30 jours. |
| `-perm 644` | Fichiers ayant les permissions exactes `644`. |
| `-user robert` | Fichiers appartenant à l’utilisateur `robert`. |
| `-group staff` | Fichiers appartenant au groupe `staff`. |
| `-empty` | Fichiers ou dossiers vides. |
| `-delete` | Supprime les éléments trouvés (à utiliser avec précaution). |
| `-exec <commande> {} \;` | Exécute une commande sur chaque élément trouvé. |

---

## 4. Exemples pratiques

### 4.1. Rechercher un fichier par extension
```bash
find /home/robert -type f -name "*.py"
```
➡️ Liste tous les fichiers Python dans le dossier de `robert`.

### 4.2. Trouver les fichiers récents
```bash
find /home/robert/Documents -mtime -3
```
➡️ Affiche les fichiers modifiés au cours des trois derniers jours.

### 4.3. Supprimer tous les fichiers temporaires
```bash
find /home/robert/tmp -type f -name "*.tmp" -delete
```

### 4.4. Rechercher des fichiers volumineux
```bash
find /home/robert -type f -size +50M
```

### 4.5. Rechercher des fichiers vides
```bash
find /home/robert -empty
```

### 4.6. Trouver les fichiers appartenant à un utilisateur spécifique
```bash
find / -user robert 2>/dev/null
```
> L’option `2>/dev/null` masque les messages d’erreur liés aux permissions.

### 4.7. Exécuter une commande sur les résultats
```bash
find /home/robert/scripts -type f -name "*.sh" -exec chmod +x {} \;
```
➡️ Rend tous les scripts exécutables dans le dossier `scripts`.

---

## 5. Exercices pratiques

### Objectif pédagogique
Maîtriser la recherche et la manipulation de fichiers avec `find` sur Raspberry Pi.

### Contexte
Les exercices se feront avec l’utilisateur **`robert`** et le répertoire **`/home/robert/`**.

---

### Exercice 1 — Rechercher des fichiers Python
1. Créez quelques fichiers de test :
   ```bash
   touch /home/robert/test1.py /home/robert/test2.txt /home/robert/code.py
   ```
2. Trouvez uniquement les fichiers Python :
   ```bash
   find /home/robert -type f -name "*.py"
   ```

---

### Exercice 2 — Identifier les fichiers récents
1. Modifiez un fichier récemment :
   ```bash
   echo "Dernière mise à jour" >> /home/robert/test1.py
   ```
2. Recherchez les fichiers modifiés dans les 24 dernières heures :
   ```bash
   find /home/robert -mtime -1
   ```

---

### Exercice 3 — Supprimer des fichiers temporaires
1. Créez un répertoire `tmp` avec des fichiers :
   ```bash
   mkdir /home/robert/tmp
   touch /home/robert/tmp/fichier1.tmp /home/robert/tmp/fichier2.tmp
   ```
2. Supprimez-les avec `find` :
   ```bash
   find /home/robert/tmp -type f -name "*.tmp" -delete
   ```

---

### Exercice 4 — Exécuter une action sur les résultats
1. Créez un dossier `scripts/` :
   ```bash
   mkdir /home/robert/scripts
   touch /home/robert/scripts/test.sh
   ```
2. Rendez tous les scripts exécutables :
   ```bash
   find /home/robert/scripts -type f -name "*.sh" -exec chmod +x {} \;
   ```

---

### Exercice 5 — Trouver les gros fichiers
1. Téléchargez ou créez un fichier volumineux (>10 Mo).  
2. Recherchez tous les fichiers supérieurs à 10 Mo :
   ```bash
   find /home/robert -type f -size +10M
   ```

---

## 6. Bonnes pratiques

- Toujours **tester** vos commandes `find` sans `-delete` avant de les exécuter définitivement.  
- Redirigez les erreurs vers `/dev/null` si vous n’avez pas les droits sur certains répertoires.  
- Combinez `find` avec d’autres outils (`grep`, `xargs`, `tar`) pour des opérations complexes.  
- Sur Raspberry Pi, attention à ne pas exécuter `find /` sans filtres — cela peut être long et gourmand en ressources.

---

## 7. Combinaisons utiles

| Commande | Utilité |
|:----------|:---------|
| `find /home/robert -type f -name "*.log" -mtime +7 -delete` | Supprime les anciens journaux (>7 jours). |
| `find /home/robert -perm 777` | Liste les fichiers avec des permissions dangereuses. |
| `find /home/robert -type f -exec grep -l "mot_clef" {} \;` | Recherche un mot-clé dans les fichiers. |
| `find /home/robert -size +100M -exec du -h {} \;` | Affiche la taille des gros fichiers trouvés. |

---

## 8. Références

- `man find`
- GNU Findutils Documentation : [https://www.gnu.org/software/findutils/](https://www.gnu.org/software/findutils/)
- Tutoriel LinuxCommand.org : [http://linuxcommand.org/lc3_man_pages/find1.html](http://linuxcommand.org/lc3_man_pages/find1.html)
