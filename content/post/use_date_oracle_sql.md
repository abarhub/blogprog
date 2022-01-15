+++
title = "Gestion des dates en oracle "
date = "2020-10-05"
description = "Gestion des dates en oracle "
tags = ["sql"]
+++


```sql
-- affichage de dates
select to_char( mon_champs, 'dd-mm-yyyy hh24:mi:ss' ) from ma_table;

-- affichage de la date et de l'heure de la session
ALTER SESSION SET NLS_DATE_FORMAT = 'dd-mm-yyyy hh24:mi:ss';

-- insertion d'une date dans un champs
insert into ma_table(ID, START_DATE) values (3,TO_DATE('20200301','YYYYMMDD'));

-- recherche de données entre deux dates
select * from ma_table where START_DATE BETWEEN TO_DATE('28-02-2014 10:15:00', 'dd-mm-yyyy hh24:mi:ss') AND TO_DATE('20-06-2014 16:34:00', 'dd-mm-yyyy hh24:mi:ss');
```
