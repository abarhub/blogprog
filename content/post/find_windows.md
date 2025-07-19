+++
title = "Recherche d'une chaine de caractère sous windows en bat et en Powershell ou avec des outils"
date = "2024-03-17"
description = "Recherche d'une chaine de caractère sous windows en bat et en Powershell ou avec des outils"
tags = ["cli","shell","windows"]
summary = "Recherche d'une chaine de caractère sous windows en bat et en Powershell ou avec des outils"
+++
# Recherche windows

## DOS (cmd)

Pour recherche les fichiers contenants une chaine de caractère, la commande est :
```bat
findstr "machaine" *.*
```
L'option /I permet de faaire une recherche insensible à la casse.

## Powershell

Pour rechercher les fichiers contenant une chaine de caractère :
```powershell
Get-ChildItem C:\temp -Filter *.log -Recurse | Select-String "machaine"
```
Cela fait une recherche récursive. Si ce n'est pas récursif, la commande est :
```powershell
Select-String -Path C:\temp\*.log -Pattern "machaine"
```

Pour rechercher les fichiers qui ont une extention de façon récursive :
```powershell
Get-ChildItem -Path "C:\code\" -Filter *.js -r -File
```

# Outils

## RipGrep

RipGrep permet de faire les recherches. L'outils est [ici](https://github.com/BurntSushi/ripgrep).

```shell
rg "machaine" -g '*.java' "C:\code\"
```

Pour rechercher par nom de fichier :
```shell
rg --files | rg -i ".java$"
```

## FD

La recherche avec FD peut être fait sur le nom du fichier. L'outils est [ici](https://github.com/sharkdp/fd).

Exemple : 
```shell
fd "\.java$" C:\code\
```
La recherche est une expression régulière.
                    