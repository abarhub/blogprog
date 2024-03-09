+++
title = "Récupération du répertoire du script BAT"
date = "2023-03-09"
description = "Récupération du répertoire du script BAT"
tags = ["bat","dos"]
summary = "Récupération du répertoire du script BAT"
+++
# Répertoire du script BAT

Pour récupérer le répertoire du script en cours en BAT, la variable est `%~dp0`. pour enlever le \ à la fin, la variable est `%~dp0:~0,-1%`

Exemple :
```bat
SET mypath=%~dp0
echo %mypath:~0,-1%
```

                    