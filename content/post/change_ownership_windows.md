+++
title = "Devenir propriété d'un répertoire sous windows"
date = "2022-11-27"
description = "Devenir propriété d'un répertoire sous windows"
tags = ["windows"]
summary = "Devenir propriété d'un répertoire sous windows"
+++
# Devenir propriété d'un répertoire sous windows

pour devenir propriétaire du répertoire c:\monrepertoire sous windows, il faut executer la commande :
```shell
takeown.exe /f c:\monrepertoire /r
```

Cela permet de régler les erreur avec git du style :
```shell
fatal: unsafe repository ('c:/monrepertoire' is owned by someone else)
To add an exception for this directory, call:

git config --global --add safe.directory c:/monrepertoire
```
                    