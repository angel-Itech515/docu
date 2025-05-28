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

# Problema alarmes

Si apareixen logs d'aquest estil:
```
2025/05/09 20:33:59.3026;	Error generaSQLAlarma_CondicionHija(80524): Referencia a objeto no establecida como instancia de un objeto.
2025/05/09 20:35:42.2377;	Error compruebaAlarmas_Condiciones(80524): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ') AS AdAT80524' at line 1 ####### SQL: SELECT  IF(IFNULL(SUM(ESTADO),0)=0,1,0) AS ESTADO, IFNULL(SUM(ESTADO),0) AS CANTIDAD, IF(IFNULL(SUM(ESTADO),0)=0,100,SUM(ESTADO)*100/0) AS PORCENTAJE  FROM () AS AdAT80524
2025/05/09 21:00:32.3411;	Error generaSQLAlarma_CondicionHija(80492): Referencia a objeto no establecida como instancia de un objeto.
2025/05/09 21:02:15.2490;	Error compruebaAlarmas_Condiciones(80492): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ') AS AdAT80492' at line 1 ####### SQL: SELECT  IF(IFNULL(SUM(ESTADO),0)>0,1,0) AS ESTADO, IFNULL(SUM(ESTADO),0) AS CANTIDAD, IF(IFNULL(SUM(ESTADO),0)>0,100,SUM(ESTADO)*100/0) AS PORCENTAJE  FROM () AS AdAT80492
2025/05/09 21:02:15.2490;	Error generaSQLAlarma_CondicionHija(80516): Referencia a objeto no establecida como instancia de un objeto.
2025/05/09 21:03:58.1695;	Error compruebaAlarmas_Condiciones(80516): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ') AS AdAT80516' at line 1 ####### SQL: SELECT  IF(IFNULL(SUM(ESTADO),0)>0,1,0) AS ESTADO, IFNULL(SUM(ESTADO),0) AS CANTIDAD, IF(IFNULL(SUM(ESTADO),0)>0,100,SUM(ESTADO)*100/0) AS PORCENTAJE  FROM () AS AdAT80516
2025/05/09 21:03:58.1785;	Error generaSQLAlarma_CondicionHija(80524): Referencia a objeto no establecida como instancia de un objeto.
2025/05/09 21:05:40.7202;	Error compruebaAlarmas_Condiciones(80524): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ') AS AdAT80524' at line 1 ####### SQL: SELECT  IF(IFNULL(SUM(ESTADO),0)=0,1,0) AS ESTADO, IFNULL(SUM(ESTADO),0) AS CANTIDAD, IF(IFNULL(SUM(ESTADO),0)=0,100,SUM(ESTADO)*100/0) AS PORCENTAJE  FROM () AS AdAT80524
```
Poden ser condicions orfes des del program usant ctrl+H.
Les id que et marque solen estar dins la taula alarmas, més info en (extreta des del codi font del PV):
```SQL
SELECT 
    `A`.*, 
    `IA`.*, 
    `IA`.`ID` AS IDREAL, 
    `T`.`Rate`, 
    `T`.`Selected`, 
    `T`.Property1,
    `T`.Property2,
    `T`.Property3,
    `T`.Property4
FROM 
    `alarmas` AS `A`
    INNER JOIN `tbitemalarm` AS `IA` ON `A`.`itemAlarm` = `IA`.`idItem`
    LEFT JOIN `tbtag` AS `T` ON `T`.`idtag` = `A`.`IdTagSalida`
WHERE 
    `A`.`IsAlarm` = 2;
```
