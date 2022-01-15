+++
title = "Commandes sous dos "
date = "2021-03-05"
description = "Commandes sous dos "
tags = ["dos", "windows", "shell", "bat"]
+++


```bat
rem Pour extraire une partie du contenu d'une variable, la syntaxe est :
echo %date:~6,4%
rem résultat:
rem 2021

rem pour remplacer un caractere par un autre :
echo %time: =0%
rem résultat:
rem 08:48:50,13


rem Pour récupérer la date du jour (ne fonctionne qu'en france) :
echo %date:~6,4%%date:~3,2%%date:~0,2%
rem résultat:
rem 20210131

rem Pour récupérer l'heure (il faut remplacer l'espace par un 0 si l'heure est inferieure à 10) :
set heure=%time:~0,2%-%time:~3,2%-%time:~6,2%
echo %heure: =0%
rem résultat:
rem 08-52-01

rem Pour mettre dans une variable la date et l'heure avec un format compatible pour un nom de fichier :
set dateheure=%date:~6,4%-%date:~3,2%-%date:~0,2%_%time:~0,2%-%time:~3,2%-%time:~6,2%
set dateheure=%dateheure: =0%
echo %dateheure%
rem résultat:
rem 2021-01-31_08-54-57
```
