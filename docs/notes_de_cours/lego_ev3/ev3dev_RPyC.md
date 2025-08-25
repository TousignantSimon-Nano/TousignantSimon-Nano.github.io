# Contrôle à distance à l'aide du module python RPyC (Remote Python Control)

Commande d'un autre Ev3 ou d'un téléphone

-- Télécommande

Commande à partir d'un PC

-- Besoin de capacités de calcul supplémentaire, ex résolution de cube Rubic

## Module RPyC (Remote Python Control)

Version 3.3.0 de RPyC déjà installée avec ev3dev

Une version similaire doit être utilisée sur le client.  ATTENTION 3.3.0 ne supporte pas Python 3.7 et plus - une modification doit être apportée pour être compatible avec les Python récents (_async_ est maintenant un mot clé réservé)

# Documentation RPyC

RPyC avec ev3dev: <https://github.com/ev3dev/ev3dev-lang-python/blob/ev3dev-stretch/docs/rpyc.rst>

Doc RPyC: <https://rpyc.readthedocs.io/>

# Installation sur ev3dev

<pre>

echo "[Unit]
Description=RPyC Classic Service
After=multi-user.target

[Service]
Type=simple
ExecStart=/usr/bin/rpyc_classic.py

[Install]
WantedBy=multi-user.target" > rpyc-classic.service


sudo mv rpyc-classic.service /lib/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable rpyc-classic.service
sudo systemctl start rpyc-classic.service

</pre>

# Installation sur PC

Créez un nouvel venv avec votre Python

<pre>
python3 -m venv ev3dev
./ev3dev/bin/activate
</pre>

(ev3dev/Scripts/activate dans PowerShell)

Installez la version 3.3.0 de rpyc

> pip install rpyc==3.3.0

Écraser le contenu du package rpyc dans lib/site-packages avec le code modifié pour Python 3.7 et plus

[rpyc-3.3.0-mod](https://cegepvicto.sharepoint.com/:u:/s/Section_31416/EaSgb2WDuqNBp8A7tOWczpABCe3ZcWbZ-h8Uz_seT3MMog?e=mVVPhZ)


# Exemple de code pour allumer les leds à distance
 
<pre>
import rpyc
conn = rpyc.classic.connect('X.X.X.X')
ev3dev2_led = conn.modules['ev3dev2.led']
leds = ev3dev2_led.Leds()
leds.set_color("LEFT", "RED")
leds.set_color("RIGHT", "RED")
</pre>
 
 

