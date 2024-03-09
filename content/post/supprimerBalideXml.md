+++
title = "Supprimer une balise xml et son contenu grace a une regex en Java"
date = "2024-03-09"
description = "Supprimer une balise xml et son contenu grace a une regex en Java"
tags = ["java","xml"]
summary = "Supprimer une balise xml et son contenu grace a une regex en Java"
+++
# Supprimer balise XML avec une Regex

Pour supprimer une balise et son contenu dans un document xml en utilisant une regex :
```Java
xmlRequest=xmlRequest.replaceAll("<Address>[\\s\\S]*?</Address>","");
```
C'est en Java, mais cela fonctionne dans d'autres langages. Si la balise est présente plusieurs fois, ça les suppriment tous. Code trouvé [ici](https://stackoverflow.com/a/42894913)
                    