+++
title = "Supprime la contrainte not null d'une colonne dont le nom de la contrainte n'est pas connue. Spécifique à Oracle"
date = "2025-03-22"
description = "Supprime la contrainte not null d'une colonne dont le nom de la contrainte n'est pas connue. Spécifique à Oracle"
tags = []
summary = "Supprime la contrainte not null d'une colonne dont le nom de la contrainte n'est pas connue. Spécifique à Oracle"
+++
-- suppression de la contrainte not null du champs mon_schema.ma_table.mon_champs
declare
    fName varchar2(255 char);
begin
    SELECT x.constraint_name into fName FROM all_constraints x
                                             JOIN all_cons_columns c ON
                                c.table_name = x.table_name AND c.constraint_name = x.constraint_name
    WHERE x.table_name = 'ma_table' AND x.OWNER='mon_schema' AND x.constraint_type = 'C' AND c.column_name ='mon_champs';

    if fName is not null THEN
       execute immediate 'ALTER TABLE "mon_schema"."ma_table" DROP CONSTRAINT ' || fName;
    end if;
end;
/
                    