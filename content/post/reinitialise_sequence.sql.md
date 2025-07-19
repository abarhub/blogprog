+++
title = "Réinitialisation d'une sequence par rapport à l'id d'une table"
date = "2025-03-22"
description = "Réinitialisation d'une sequence par rapport à l'id d'une table"
tags = ["sql","oracle"]
summary = "Réinitialisation d'une sequence par rapport à l'id d'une table"
+++
```sql
DECLARE
    v_max_id NUMBER;
BEGIN
    -- Récupèrer le dernier ID utilisé dans la table
    SELECT COALESCE(MAX(id), 0) INTO v_max_id FROM mon_schema.ma_table;

    -- Repositionner la séquence pour démarrer au bon endroit
    EXECUTE IMMEDIATE 'ALTER SEQUENCE mon_schema.SEQ_ma_sequence RESTART START WITH ' || (v_max_id + 1) ;

    DBMS_OUTPUT.PUT_LINE('Séquence repositionnée à ' || (v_max_id + 1));
END;
/
```
                    