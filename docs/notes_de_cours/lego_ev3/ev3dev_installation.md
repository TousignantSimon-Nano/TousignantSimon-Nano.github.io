# Installation ev3dev

Les étapes sont disponibles sur le site officiel de ev3dev: <https://www.ev3dev.org/docs/getting-started/>

Suivez les étapes pour LEGO MINDSTORMS EV3

La dernière image date d'avril 2020. Vous pouvez utiliser Win32DiskImager pour écrire l'image sur la carte.

==Attention== il faut écrire le fichier .img, pas le .zip!

Étape 5: connexion réseau - utiliser [Connecting to the Internet via USB](https://www.ev3dev.org/docs/tutorials/connecting-to-the-internet-via-usb/)

Je recommande de laisser le EV3 finir son démarrage avant de le connecter au PC.  Ensuite le brancher et laisser le pilote de périphérique Remote NDIS s'installer.

Une fois le partage de connexion activé, aller dans Wireless and Networking -> All Network Connections -> Wired, déconnecter puis reconnecter: vous devriez obtenir une adresse IPv4 dans un autre "subnet" privé, accessible de votre PC seulement.

Une fois le SSH fonctionnel, je vous recommande de suivre les instructions pour mettre la base de packages "apt" à jour. 
