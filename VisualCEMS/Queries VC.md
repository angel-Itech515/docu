## INI
```SQL
select * from tbtag;
select * from tbparamgenerales;
select * from tbinstancia;
select * from tbitemcsv;
```
[[taula tbtag]]
[[taula xt_configtags]]
## Dades interficie lectura i tags configuració
```SQL
select t.name,x.* from t_tempi x left join tbtag t on idtag=id_parametro where name like '%%';
select t.name,t.interface,x.* from t_tempi x left join tbtag t on idtag=id_parametro;

select t.name,x.* from t_temp x left join tbtag t on idtag=id_parametro where name like '%%' order by dia desc limit 10;
select t.name,t.interface,x.* from t_temp x left join tbtag t on idtag=id_parametro order by dia desc limit 10;

SELECT *
FROM y_2025 y
ORDER BY dia DESC limit 1;

select t.name,x.* from xt_configtags x left join tbtag t on idtag=id_parametro where name like '%%';
select * from xt_configtags where id_parametro in(select idtag from tbtag where name like '%%');
```
## Dades taules year
```SQL
SELECT t.name, z.*
FROM z_2025_2 z
LEFT JOIN tbtag t ON t.idtag = z.id_parametro
WHERE t.name = 'NOX.IN' order by dia desc limit 100000;

SELECT t.name, y.*
FROM y_2024 y
LEFT JOIN tbtag t ON t.idtag = y.id_parametro
WHERE t.name = 'NOX-30MIN-MCTV' AND caracter_validacion='VA';

SELECT t.name, y.*
FROM y_2025 y
LEFT JOIN tbtag t ON t.idtag = y.id_parametro
WHERE t.name = 'NOX.DPN' order by dia desc limit 100000;

SELECT *
FROM y_2025 y
WHERE id_parametro=(select idtag from tbtag where name = 'STAT1.SRC') and dia > '2025-02-14 10:51:00' and dia < '2025-02-19 07:39:00';
```
## Inserts de dades
```SQL
INSERT IGNORE INTO y_2024 (dia, id_parametro, valor, valor_corregido, caracter_validacion)  
VALUES  
    ('2024-11-30 23:00:00', 285, 0, 0, 'VD'),  
    ('2024-11-30 23:00:00', 286, 0, 0, 'VD'),  
    ('2024-11-30 23:00:00', 287, 0, 0, 'VD'),  
    ('2024-11-30 23:00:00', 288, 0, 0, 'VD'),  
    ('2024-11-30 23:00:00', 289, 0, 0, 'VD');
    
-- Entre BD
INSERT IGNORE INTO pv22_tracjusa_foco1_2025.z_2025 (dia, id_parametro, valor, valor_corregido, caracter_validacion)
SELECT dia, id_parametro, valor, valor_corregido, caracter_validacion
FROM pv22_tracjusa_foco1.z_2025;
```
## FOCO-STATUS.IN update a N, posa tota la planta a fallo
```SQL
-- Sent 2 foco-status i 4 contaminant-status
select * from z_2025
where dia > '2025-01-14 14:30:00'
and dia < '2025-01-15 13:05:00'
and id_parametro=2
and valor_corregido=4;

-- UPDATE z_2025
SET valor = -1
WHERE dia > '2025-01-14 14:30:00'
  AND dia < '2025-01-15 13:05:00'
  AND id_parametro = 2
  AND valor_corregido = 4;
```
## UPDATE valors i CV a partir d'un altre contaminant si esta a null, cas ciments molins
```SQL
SELECT target.dia, target.id_parametro, target.valor, target.valor_corregido, target.caracter_validacion,
       source.caracter_validacion AS nuevo_caracter_validacion
FROM Y_2025 AS target
JOIN Y_2025 AS source
    ON target.dia = source.dia
    AND source.id_parametro = 24001349
WHERE target.id_parametro = 24001807
  AND target.valor = 0;

-- UPDATE Y_2025 AS target
JOIN Y_2025 AS source
    ON target.dia = source.dia
    AND source.id_parametro = 24001349
SET target.valor = 0,
    target.valor_corregido = 0,
    target.caracter_validacion = source.caracter_validacion
WHERE target.id_parametro = 24001807
  AND target.valor IS NULL;
```

# VAs anuals
```SQL
select * from xt_configtags where id_parametro in(select idtag from tbtag where name like '%%');
select t.name,x.* from xt_configtags x left join tbtag t on idtag=id_parametro where name like 'NOX%VA%';

SELECT t.name, y.*
FROM y_2024 y
LEFT JOIN tbtag t ON t.idtag = y.id_parametro
WHERE t.name = 'NOX-30MIN-MCTV' AND caracter_validacion='VA';

SELECT t.name, y.*
FROM y_2024 y
LEFT JOIN tbtag t ON t.idtag = y.id_parametro
WHERE t.name = 'NOX-COQUE-30MIN-MCTV' AND caracter_validacion='VA';

SELECT t.name, MAX(valor)
FROM y_2024 y
LEFT JOIN tbtag t ON t.idtag = y.id_parametro
WHERE t.name = 'TOT-FA-CONT-COQUE';

SELECT t.name, y.*
FROM y_2024 y
LEFT JOIN tbtag t ON t.idtag = y.id_parametro
WHERE t.name = 'TOT-FA-CONT-COQUE' AND VALOR=9;
-- 2024-08-26 19:30:00
-- 2024-11-06 22:00:00

SELECT t.name, y.*
FROM y_2024 y
LEFT JOIN tbtag t ON t.idtag = y.id_parametro
WHERE t.name = 'NOX-COQUE-30MIN-MCTV' AND caracter_validacion='VA';

select * from tbtag where name like 'tot-fa%';
```
