+++
title = "Exemple de requete sql pour détruire toutes les tables d'un schéma"
date = "2021-01-07"
description = "Exemple de requete sql pour détruire toutes les tables d'un schéma"
tags = ["sql"]
+++

Exemple de requete sql pour détruire toutes les tables d'un schéma :
```sql
select 'drop table '||table_name||' cascade constraints;' from user_tables;
```
