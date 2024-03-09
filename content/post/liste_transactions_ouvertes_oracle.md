+++
title = "Lister les transactions ouvertes en Oracle"
date = "2024-03-09"
description = "Lister les transactions ouvertes en Oracle"
tags = ["sql","oracle"]
summary = "Lister les transactions ouvertes en Oracle"
+++
# Liste des transactions ouvertes en Oracle

Pour lister les sessions Oracle, il faut executer la requete suivante :
```sql
select s.inst_id, s.sid, s.serial#, s.username,
       s.program, s.osuser, s.status session_status,
       s.sql_id, t.status tran_status, 
       t.start_time tran_start, t.used_ublk used_undo_blocks, 
       t.used_urec used_undo_recs
  from gv$session s, gv$transaction t
 where t.addr = s.taddr;
```
                    