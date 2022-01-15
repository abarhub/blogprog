+++
title = "Création d'un composant avec un module et une route "
date = "2020-09-16"
description = "Création d'un composant avec un module et une route "
tags = ["shell", "angular"]
+++

Voici les commandes pour créer un module, puis un composant associé a ce module :
```shell
ng generate module app/modules/monmodule --routing=true
ng generate component app/modules/monmodule/moncomposant -m=app/modules/monmodule
```
