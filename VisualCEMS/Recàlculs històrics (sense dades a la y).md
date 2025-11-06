La idea es crear els triggers dels tags VC que encara no existeixen, es suposa que has de plenar una linia per cada tag.
Fer-ho a mà no té sentit. Per tant repliques les dades en data actual generant nous triggers, el recàlcul arregla les dades incorporades incorrectes que han servit com a trigger.

!!!!! Si falla per t_temp2 full hi ha algun espai de dades buit enorme, simplement para recalcul i plena buit.

```SQL
-- DPN 1
insert into y_2025 (dia, id_parametro, valor, valor_corregido, caracter_validacion)
select '2024-12-31 23:00:00', id_parametro, valor, valor_corregido, caracter_validacion
from y_2025 where dia = '2025-07-01 23:00:00';

-- DPN 2
insert into y_2024 (dia, id_parametro, valor, valor_corregido, caracter_validacion)
select '2024-12-31 22:59:00', id_parametro, valor, valor_corregido, caracter_validacion
from y_2025 where dia = '2025-07-01 22:59:00';

-- 30MIN
insert into y_2024 (dia, id_parametro, valor, valor_corregido, caracter_validacion)
select '2024-12-31 22:30:00', id_parametro, valor, valor_corregido, caracter_validacion
from y_2025 where dia = '2025-07-01 22:30:00';

-- 60MIN
insert into y_2024 (dia, id_parametro, valor, valor_corregido, caracter_validacion)
select '2024-12-31 22:00:00', id_parametro, valor, valor_corregido, caracter_validacion
from y_2025 where dia = '2025-07-01 22:00:00';

-- MLTs
insert into y_2024 (dia, id_parametro, valor, valor_corregido, caracter_validacion)
select '2024-12-30 22:00:00', id_parametro, valor, valor_corregido, caracter_validacion
from y_2025 where dia = '2025-07-01 22:00:00';
```
