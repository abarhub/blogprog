+++
title = "Commande find"
date = "2025-07-19"
description = "Commande find"
tags = []
summary = "Commande find"
+++
La commande find 

```shell
find . -name "main.c" -print
```

les parametres de recherche :
* `-name XXX` : le nom du fichier recherche
* `-path XXX` : recherche sur le chemin complet c-a-d le nom du fichier et le répertoire
* `-maxdepth n`: rechercher sur une profondeur maximale de n

les parametres action :
* `-print` : affiche le résultat. si aucune action n'est renseigné
* `-exec XXX` : execute la commande sur chaque fichier retrouvé, le parametre est `{}`. par exemple : `find /home/debianos -user debianos -type f -exec ls -l {} \;`
                    