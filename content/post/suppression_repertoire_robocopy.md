+++
title = "suppression d'une grand arborescence sous windows rapidement (robocopy)"
date = "2024-02-27"
description = "suppression d'une grand arborescence sous windows rapidement (robocopy)"
tags = ["bat","dos","robocopy"]
summary = "suppression d'une grand arborescence sous windows rapidement (robocopy)"
+++
# Suppression des répertoires

La suppression d'une grande arborescence de répetroire est très lente avec l'explorateur. 
Pour supprimer des répertoires, de façon plus rapide, il y a la commande robocopy.
Pour supprimer le répertoire c:\test, il faut créer un répertoire vide c:\empty, puis lancer :
```batch
robocopy c:\empty c:\test /purge
```
ou
```batch
robocopy c:\empty c:\test /MIR
```

La différence est que si le répertoire c:\test existe, les ACL ne seront pas modifiés avec la commande /MIR
                    