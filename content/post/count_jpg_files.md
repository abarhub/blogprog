+++
title = "Compter les fichiers jpeg par répertoire"
date = "2022-03-20"
description = "Compter les fichiers jpeg par répertoire"
tags = ["shell", "linux", "image", "jpg"]
summary = "Compter les fichiers jpeg par répertoire"
+++

Pour lister les répertoires qui ont des fichiers jpeg :
```shell
find / -iname "*.jpg" -exec dirname '{}' \; | uniq -c >res.txt
```
Apres, pour trié cette liste, c'est :
```shell
cat res.txt | sort -n
```

