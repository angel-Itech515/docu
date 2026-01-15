La idea es crear els triggers dels tags VC que encara no existeixen, es suposa que has de plenar una linia per cada tag.
Fer-ho a mà no té sentit. Per tant repliques les dades en data actual generant nous triggers, el recàlcul arregla les dades incorporades incorrectes que han servit com a trigger.

!!!!! Si falla per t_temp2 full hi ha algun espai de dades buit enorme, simplement para recalcul i plena buit.

```SQL
-- insert ignore into y_2026 (dia, id_parametro, valor, valor_corregido, caracter_validacion)
select '2025-12-31 23:00:00', idtag, 0, 0, 'V'
from tbtag where interface='VC';
```
