# Exercices : Configuration IP fixe sur Raspberry Pi

## Contexte
Dans cet exercice, chaque étudiant va configurer son Raspberry Pi pour avoir une **adresse IP fixe** dans une plage définie, se synchroniser avec le groupe et tester la connectivité.

---

## 1. Configuration IP fixe

### Objectifs
- Définir une **adresse IP fixe** entre `192.168.61.100` et `192.168.61.200`.  
- Masque réseau : `/23` (255.255.254.0).  
- Les étudiants doivent **s’organiser eux-mêmes** pour savoir qui prend quelle adresse.  
- Serveurs DNS : `8.8.8.8` et `1.1.1.1`.  

### Tâches
1. Identifier les fichiers dans `/etc` permettant de définir une IP fixe.  
   - Exemple : `/etc/dhcpcd.conf`, `/etc/network/interfaces` (selon la version de Raspbian).  
2. Modifier le fichier choisi pour configurer :  
   - Adresse IP  
   - Masque réseau (/23)  
   - Passerelle par défaut (si nécessaire)  
   - DNS primaire et secondaire  

> ⚠️ Chaque étudiant doit choisir une IP différente dans la plage pour éviter les conflits.

---

## 2. Vérification de l’adresse IP
- Vérifier l’adresse IP configurée avec :
```bash
ip addr show
ifconfig
ip a
# autre commandes possible.
```

## 3. Test des DNS

Vérifier que les DNS fonctionnent :
```bash
nslookup google.com
ping www.google.com
```
## 4. Test de téléchargement

Télécharger un fichier depuis Internet pour vérifier la connectivité :
```bash  
wget https://sampletestfile.com/wp-content/uploads/2023/05/1MB.png  
```

## 5. Points à noter  

Les étudiants doivent documenter dans un fichier texte :  

Quelle IP a été choisie  

Quel(s) fichier(s) /etc a été modifié après modification de l'adresse ip ( la commande grep peut aider )  

Les commandes utilisées pour vérifier l’adresse IP et le DNS

Le résultat du test wget

