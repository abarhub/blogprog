+++
title = "Suppression du lock sur une table Oracle"
date = "2024-03-09"
description = "Suppression du lock sur une table Oracle"
tags = ["sql","oracle"]
summary = "Suppression du lock sur une table Oracle"
+++
# Table locké

Pour vérifier si une table est locké en Oracle, il faut executer la requete sql avec un compte system :
```sql
-- Query to Get List of all locked objects
SELECT B.Owner, B.Object_Name, A.Oracle_Username, A.OS_User_Name  
FROM V$Locked_Object A, All_Objects B
WHERE A.Object_ID = B.Object_ID ;
```

Ensuite il faut récupérer les identifants avec la requete suivante, en remplacant `NOM_DU_SCHEMA` par le nom du schéma concerné :
```sql
-- Query to Get List of locked sessions        
select SID,SERIAL#,INST_ID from gv$session a  where schemaname = 'NOM_DU_SCHEMA';
```

Enfin, il faut arreter le lock, en utilisant le résultat de la requete précédente :
```sql
-- Statement to Kill the session [pass values in the same order and append @ for inst_id]
alter system kill session '314,26513,@1';
```

Code trouvé [ici](https://dba.stackexchange.com/a/245861)



                    