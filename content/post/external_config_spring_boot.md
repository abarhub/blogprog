+++
title = "Externalisation de la configuration avec spring boot"
date = "2021-06-29"
description = "Externalisation de la configuration avec spring boot"
tags = ["spring boot", "configuration"]
summary = "Externalisation de la configuration avec spring boot"
+++

* Exemple avec le paramtre spring.config.location :
```shell
java -jar app.jar --spring.config.location=file:///Users/home/config/jdbc.properties
```
* Autre exemple avec les paramètres spring.config.location et spring.config.name :
```shell
java -jar app.jar --spring.config.name=application,jdbc --spring.config.location=file:///Users/home/config
```
* Exemple avec une variable d'environnement :
```shell
export SPRING_CONFIG_LOCATION=file:///Users/home/config
java -jar app.jar
```
* Exemple avec spring.config.import :
```shell
spring.config.import=file:./additional.properties,optional:file:/Users/home/config/jdbc.properties
```
* Exemple avec spring.config.additional-location :
```shell
java -jar app.jar --spring.config.additional-location=file:///Users/home/config/
```
Voir ici :
https://www.baeldung.com/spring-properties-file-outside-jar
https://docs.spring.io/spring-boot/docs/1.0.1.RELEASE/reference/html/boot-features-external-config.html