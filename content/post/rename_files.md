+++
title = "Renommage de fichiers"
date = "2023-02-10"
description = "Renommage de fichiers"
tags = ["linux"]
summary = "Renommage de fichiers"
+++
# Renommage de fichiers

```shell
find . -name 'node_modules' -type d -prune


find . -name 'node_modules' -type d -prune -exec rm -rf '{}' +



find . -name 'node_modules' -o -name 'target' -type d -prune


find . -name 'node_modules' -o -name 'target' -type d -prune -exec rm -rf '{}' +


find . -name 'node_modules' -o -name 'target' -o -name '.angular' -type d -prune -exec rm -rf '{}' +


find . -name 'node_modules' -type d -prune -exec rm -rf '{}' +



find . -type f -name "*.zip" -exec sh -c 'x="{}"; mv "$x" "${x}_renamed.txt"' \;

find . -type f -name "*.7z" >liste_7z_files.txt


find . -type f -name "*.7z" -exec sh -c 'x="{}"; mv "$x" "${x}_renamed.txt"' \;

find . -type f -exec rename -n -e 's/(.*)\-DESKTOP\-9EI0FN7(.*)/$1$2/' {} \;

```
                    