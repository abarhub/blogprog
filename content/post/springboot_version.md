+++
title = "Récupérer la version avec spring boot"
date = "2022-02-20"
description = "Récupérer la version avec spring boot"
tags = ["java", "spring boot", "version", "maven", "build"]
summary = "Récupérer la version avec spring boot"
+++
Le plus simple c'est de lire le fichier version.properties dans le classpath.

```Java
try(InputStream inputStream = getClass().getClassLoader().getResourceAsStream("version.properties")){
  Properties prop = new Properties();
  prop.load(inputStream);
  String version=prop.get("version","1.0.0");
  return version;
}
```

Il existe d'autres façons de faire :
* [utiliser la classe BuildProperties](https://www.vojtechruzicka.com/spring-boot-version/)
* [lire le manifest](https://stackoverflow.com/a/41791885/6577778)
* [ajouter la version dans la configuration](https://stackoverflow.com/a/3697482/6577778)

Autres solutions:
* [https://stackoverflow.com/questions/3697449/retrieve-version-from-maven-pom-xml-in-code]
* [https://www.baeldung.com/spring-boot-build-properties]