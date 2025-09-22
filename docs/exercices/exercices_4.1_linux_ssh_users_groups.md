# Exercices Linux : gestion des utilisateurs, groupes et SSH

## Exercice 1 : Création de groupes et d’utilisateurs

1. Créez les groupes suivants :
   - `administrateurs`
   - `dev`
   - `guest`

2. Créez les utilisateurs suivants avec un mot de passe temporaire :
   - `alice` dans le groupe `administrateurs`
   - `bob` dans le groupe `dev`
   - `carol` dans le groupe `guest`

3. Vérifiez que les utilisateurs sont bien dans les bons groupes.

**Commandes utiles :**
```bash
sudo groupadd <nom_groupe>
sudo useradd -m -G <groupe> <nom_utilisateur>
sudo passwd <nom_utilisateur>
id <nom_utilisateur>
```

---

## Exercice 2 : Limiter l’accès SSH pour certains utilisateurs

1. Autorisez uniquement `alice` et `bob` à se connecter via SSH.
2. Bloquez `carol` pour qu’elle ne puisse pas se connecter.

**Indice :** modifier `/etc/ssh/sshd_config` 
- Paramètres utiles : `AllowUsers`, `DenyUsers`
```bash
sudo nano /etc/ssh/sshd_config
# Exemple:
AllowUsers alice bob
```
- Redémarrez SSH :
```bash
sudo systemctl restart ssh
```

---

## Exercice 3 : Limiter l’accès SSH par groupe

1. Créez un utilisateur `dave` dans le groupe `dev`.
2. Configurez SSH pour que **tous les utilisateurs du groupe `dev`** puissent se connecter.
3. Bloquez tous les autres groupes.

**Astuce :** 
- SSH peut utiliser `AllowGroups` dans `/etc/ssh/sshd_config` :
```bash
AllowGroups dev
```

---

## Exercice 4 : Connexion SSH uniquement par clé RSA

1. Pour l’utilisateur `alice` :
   - Générez une clé RSA sur un poste client :
   ```bash
   ssh-keygen -t rsa -b 4096
   ```
   - Copiez la clé publique sur le serveur :
   ```bash
   ssh-copy-id alice@serveur
   ```
2. Configurez SSH pour que `alice` **ne puisse se connecter qu’avec sa clé RSA** et non avec un mot de passe.

**Indice :**
- Modifier `/etc/ssh/sshd_config` :
```bash
PasswordAuthentication no
```
- Redémarrer SSH :
```bash
sudo systemctl restart ssh
```

---

## Vérifications et bonus

- Vérifiez la connexion SSH pour chaque utilisateur et notez les résultats.
- Bonus : créer un utilisateur `eve` qui peut se connecter via SSH mais **uniquement depuis une IP spécifique**.

**Indices pour le bonus :**
- Regardez la directive `Match` dans `/etc/ssh/sshd_config`.
- Vous pouvez combiner `Match User eve` avec `Address <IP>`.
- N’oubliez pas de redémarrer SSH après la modification.

