# Python sur ev3dev

Guide: <https://ev3dev-lang.readthedocs.io/projects/python-ev3dev/>

Les scripts Python que vous placez sur la carte SD peuvent être exécutés dans le GUI ev3dev (Brickman) via le `File Browser`.

Vous pouvez transférer vos scripts via sftp/scp ou éditer directement via ssh avec nano/vim.  Le fichier doit être marqué comme exécutable (chmod u+x _fichier.py_)

Sur erreur à l'éxécution, un fichier d'erreur est généré dans le même répertoire de le script .py
 
Une fois le script fonctionnel, vous pouvez retirer la connexion USB pour que votre montage soit autonome.

Exemple de script:

```
#!/usr/bin/env python3
from ev3dev2.motor import LargeMotor, OUTPUT_A, SpeedPercent
from ev3dev2.sensor import INPUT_1
from ev3dev2.sensor.lego import TouchSensor
from ev3dev2.led import Leds
from ev3dev2.sound import Sound

print("Start")

sound = Sound()
sound.speak('Welcome to the E V 3 dev project!')

m = LargeMotor(OUTPUT_A)
m.on_for_rotations(SpeedPercent(75), 5)

print("Press the touch sensor to change the LED color!")

ts = TouchSensor(INPUT_1)
leds = Leds()

while True:
    if ts.is_pressed:
        leds.set_color("LEFT", "GREEN")
        leds.set_color("RIGHT", "GREEN")
    else:
        leds.set_color("LEFT", "RED")
        leds.set_color("RIGHT", "RED")

```

Liste de demos: <https://github.com/ev3dev/ev3dev-lang-python-demo>
