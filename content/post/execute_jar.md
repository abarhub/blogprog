+++
title = "Execution du premier jar trouvé"
date = "2023-06-07"
description = "Execution du premier jar trouvé"
tags = ["dos","bat"]
summary = "Execution du premier jar trouvé"
+++
Pour executer un fichier jar dans le répertoire courant, en prenant le premier jar trouvé, il faut faire 
```bat
SET mypath=%~dp0
rem echo %mypath:~0,-1%
SET REP=%mypath:~0,-1%
set filename=monjar-1.0.jar
FOR %%F IN (*.jar) DO (
 set filename=%%F
 goto next
)
:next
java -jar %REP%\%filename%
```
                    