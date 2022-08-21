+++
title = "Accès à un fichier de ressource"
date = "2020-06-18"
description = "Accès à un fichier de ressource"
tags = ["java", "xsd", "test", "classpath"]
summary = "Accès à un fichier de ressource"
+++

Accès à un fichier de ressource :

```Java
// récupération du répertoire d'un fichier ressource
File file = new File(getClass().getClassLoader().getResource("database.properties").getFile());

// lecture d'un fichier ressource
InputStream inputStream = getClass().getClassLoader().getResourceAsStream("database.properties");

// Dans les 2 cas, le fichier doit être src/main/resources/database.properties
```

Des exemples pour récupérérer le chemin :
https://stackoverflow.com/questions/15713119/java-nio-file-path-for-a-classpath-resource
