---
title: "Maven Dependancy"
date: 2021-07-18T16:21:12+01:00
draft: false
tags: ["maven"]
summary : "Affichage de la liste des dépendances"
---

Pour récupérer les dépendances d'un projet maven :
```mvn dependency:tree```

Pour récupérer les dépendances d'un projet maven, et mettre le résultat dans un fichier :
```mvn dependency:tree -DoutputFile=/path/to/file```

Pour que le résultat soit dans un format spécial :
```mvn dependency:tree -DoutputFile=/path/to/file.graphml -DoutputType=graphml```

Les sortie possibles sont :
* text
* dot
* graphml
* tgf

