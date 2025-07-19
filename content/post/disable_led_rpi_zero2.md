+++
title = "Désactivation de la led pour le raspberry pi zero 2"
date = "2025-07-16"
description = "Désactivation de la led pour le raspberry pi zero 2"
tags = []
summary = "Désactivation de la led pour le raspberry pi zero 2"
+++

Pour désactiver la led du raspberry pi zero 2, il faut lancer la commande :
```shell
shell> echo 0 | sudo tee /sys/class/leds/ACT/brightness
```

pour qu'il soit lancer au démarrage, il faut l'ajouter dans le /etc/profile.d :

```shell
shell> sudo echo >/etc/profile.d/stopled.sh <<EOL

# eteint la led du raspberry pi zero 2
echo 0 | sudo tee /sys/class/leds/ACT/brightness

EOL
```

                    