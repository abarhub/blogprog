+++
title = "description de grep"
date = "2025-07-17"
description = "description de grep"
tags = []
summary = "description de grep"
+++
# Commande grep

Recherche le text void sur les fichiers du répertoire courant
```shell
grep void 
```

Recherche dans le sous répertoire les fichiers avec l'extension `c`
```shell
grep void src/*.c
```

Affiche les numéro de lignes
```shell
grep -n void *.c
```

Recherche dans les sous répertoire
```shell
grep -r void *.c
```

Options interressante :
* A n : affiche n lignes avant
* B n : affcihe n lignes apres
* C n : affiche n lignes avant et apres
* n : affiche le numéro de ligne
* e regex : recherche suivant une regex



                    