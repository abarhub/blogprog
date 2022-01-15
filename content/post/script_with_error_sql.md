+++
title = "Stopper l'execution d'un script à la première erreur en Oracle"
date = "2020-06-18"
description = "Stopper l'execution d'un script à la première erreur en Oracle"
tags = ["sql", "plsql"]
+++

```sql
-- pour stoper l'execution à la première erreur
-- a utiliser au début d'un script
WHENEVER SQLERROR EXIT FAILURE
```
