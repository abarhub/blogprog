+++
title = "Script de création d'un schéma Mysql avec l'utilisateur "
date = "2021-01-01"
description = "Script de création d'un schéma Mysql avec l'utilisateur "
tags = ["sql", "MySQL"]
+++

Voici un exemple pour créer un utiliser MySQL et le schéma associé :
```sql
CREATE USER 'monutilisateur'@'localhost' IDENTIFIED BY '1234';

CREATE DATABASE monschema CHARACTER SET utf8 COLLATE utf8_unicode_ci;
GRANT ALL PRIVILEGES ON monschema.* TO 'monutilisateur'@'localhost';

FLUSH PRIVILEGES;
```
