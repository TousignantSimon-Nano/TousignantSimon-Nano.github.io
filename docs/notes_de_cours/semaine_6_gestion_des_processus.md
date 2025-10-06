# Gestion des processus sous Linux

## 🖥️ Affichage et surveillance

En Linux, chaque processus en cours d’exécution se voit attribuer un PID (Process ID), un identifiant unique qui permet au système et à l’utilisateur de le distinguer des autres processus. Le PID est utilisé pour gérer le processus, par exemple pour l’arrêter avec kill ou pour ajuster sa priorité avec renice.

| Commande | Fonction | Exemple / Usage |
|----------|----------|----------------|
| `ps aux` | Affiche tous les processus avec info détaillée | `ps aux | grep nginx` |
| `htop`  | Interface interactive pour trier, filtrer et gérer les processus | `htop` |
| `top`   | Affichage temps réel, moins interactif | `top` |

---

## 🔍 Recherche de processus

| Commande | Fonction | Exemple / Usage |
|----------|----------|----------------|
| `pgrep` | Recherche PID par nom de processus | `pgrep -u root sshd` |
| `pidof` | Renvoie PID d’un programme spécifique | `pidof firefox` |

---

## 🛠️ Gestion et terminaison de processus

 La commande nice (ou son ajustement via renice) contrôle la priorité CPU d’un processus. Chaque processus a une valeur de “niceness” comprise entre -20 (priorité la plus élevée) et 19 (priorité la plus faible). Plus la valeur est basse, plus le processus reçoit de temps CPU par rapport aux autres. Cette mécanique permet de gérer l’usage des ressources et d’éviter qu’un processus monopolise le CPU, garantissant ainsi une répartition plus équitable entre tous les processus du système.

| Commande | Fonction | Exemple / Usage |
|----------|----------|----------------|
| `kill` | Envoie un signal à un processus par PID | `kill 1234` (SIGTERM par défaut), `kill -9 1234` (SIGKILL) |
| `killall` | Termine tous les processus correspondant à un nom | `killall firefox`, `killall -9 nginx` |
| `kill $(pgrep -f ...)` | Combine recherche et kill par motif | `kill $(pgrep -f 'python myscript.py')` |
| `renice` | Ajuste la priorité CPU d’un processus | `renice -n 10 -p 1234` |

---

## ⚙️ Processus en arrière-plan

| Commande | Fonction | Exemple / Usage |
|----------|----------|----------------|
| `jobs` | Liste les processus en arrière-plan du shell | `jobs` |
| `fg` / `bg` | Ramène un processus en avant/arrière-plan | `fg %1`, `bg %1` |

---

## 💡 Notes complémentaires

- **Filtrage avec `grep` ou `egrep`** :  
  `ps aux | egrep 'nginx|apache2'`  

- **`htop` vs `top`** :  
  - `htop` : tri et filtrage interactif, envoi direct de signaux  
  - `top` : utile si `htop` n’est pas installé ou pour scripts automatisés  

- **Signaux fréquents pour `kill`** :  
  - `SIGTERM` (15) : demande polie d’arrêt  
  - `SIGKILL` (9) : arrêt forcé immédiat  

- **Combinaison utile** :  
  `kill $(pgrep -f 'motif_du_processus')` pour tuer plusieurs processus correspondant à un motif sur toute la ligne de commande.
