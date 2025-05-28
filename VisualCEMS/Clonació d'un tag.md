# Duplicat bbdd original (només la estructura)


### Pas 1, esborra tot excepte el contaminant a clonar

	Canvia HF pel que es vulgui clonar.

```SQL
delete from tbtag where name not like '%HF%';  
delete from tbcalculatetag where idtag not in(select idtag from tbtag);  
delete from tbambientalvle where idtag not in(select idtag from tbtag);  
delete from xt_configtags where id_parametro not in(select idtag from tbtag);  
-- Borrar totalizadores desde el program antes de seguir  
update alarmas set isalarm = 1 where isalarm =0 and nombre not like '%HF%';  
-- Ir al program y borrar condiciones huerfanas (Control + H en la pantalla de condiciones)
```

Cas especial CO:
```SQL
delete from tbtag where name not like 'CO.%' and name not like 'CO-%' and name not like '%-CO-%';
delete from tbcalculatetag where idtag not in(select idtag from tbtag);
delete from tbambientalvle where idtag not in(select idtag from tbtag);
delete from xt_configtags where id_parametro not in(select idtag from tbtag);
-- Borrar totalizadores desde el program antes de seguir
update alarmas set isalarm = 1 where isalarm =0 and nombre not like 'CO.%' and nombre not like 'CO-%' and nombre not like '%-CO-%';
```

### Pas 2, Clonar tots els registres

1. Fer un Backup de la nova configuració
2. Mirar quin és el idtag més gran de la bbdd original, afegir marge sobre aquest dins la bbdd auxiliar (ex. a Saica 24000000 -> 25000000)
3. Executar com a Script del mysql i depurar

```SQL
-- CAMBIAR el + 20000 per un nº que faci que els nous Ids no colisionin  
-- CAMBIAR  NOX pel parametre origen (En el teu cas O2SECO)  
-- CAMBIAR SO2 pel parametre desti (En el teu cas O2COMBUSTION)  
-- Incremento de ID en tbtag
UPDATE tbtag 
SET idtag = idtag + 20000;

-- Incremento de iopath solo para interfaces específicas y valores válidos
UPDATE tbtag 
SET iopath = iopath + 20000 
WHERE interface IN ('CT', 'VC') 
  AND iopath IS NOT NULL 
  AND iopath <> 0;

-- Incremento en tbcalculatetag
UPDATE tbcalculatetag 
SET idtag = idtag + 20000;

UPDATE tbcalculatetag 
SET idtagcalculation = idtagcalculation + 20000 
WHERE idtagcalculation IS NOT NULL;

-- Actualización en alarmas
UPDATE alarmas 
SET idtagsalida = idtagsalida + 20000  
WHERE idtagsalida <> 0;

UPDATE alarmas 
SET idtagprimigeneo = idtagprimigeneo + 20000 
WHERE type NOT IN (-1,6) 
  AND (idtagprimigeneo + 20000) IN (SELECT idtag FROM tbtag);

UPDATE alarmas 
SET id_parametro = id_parametro + 20000 
WHERE type = 5 
   OR (id_parametro + 20000) IN (SELECT idtag FROM tbtag);

-- tbambientalvle
UPDATE tbambientalvle 
SET idtag = idtag + 20000, 
    value = value + 20000;

-- REPLACE calculatetag con alarmas asociadas
REPLACE INTO tbcalculatetag (idtag, priority, calculationtype, begindate, typeassignment, valueassignment, BC, conditions, idtagcalculation)
SELECT 
  t.idtag,
  t.priority,
  t.calculationtype,
  t.begindate,
  t.typeassignment,
  t.valueassignment,
  t.BC,
  GROUP_CONCAT(CASE WHEN a.ID <> 20 THEN a.id + 20000 ELSE a.id END SEPARATOR '#') AS conditions,
  t.idtagcalculation
FROM tbcalculatetag t
LEFT JOIN alarmas a ON CONCAT('#', t.conditions, '#') LIKE CONCAT('%#', a.id, '#%')
GROUP BY t.idtag, t.priority, t.calculationtype, t.begindate, t.typeassignment, t.valueassignment, t.BC, t.idtagcalculation;

-- REPLACE ambientalvle con condiciones
REPLACE INTO tbambientalvle (idtag, priority, ic95, vle, value, conditions)
SELECT 
  t.idtag,
  t.priority,
  t.ic95,
  t.vle,
  t.value,
  GROUP_CONCAT(CASE WHEN a.ID <> 20 THEN a.id + 20000 ELSE a.id END SEPARATOR '#') AS conditions
FROM tbambientalvle t
LEFT JOIN alarmas a ON CONCAT('#', t.conditions, '#') LIKE CONCAT('%#', a.id, '#%')
GROUP BY t.idtag, t.priority, t.ic95, t.vle, t.value;

-- Actualización de ID en alarmas e itemalarm
UPDATE alarmas 
SET id = id + 20000, 
    itemalarm = itemalarm + 20000 
WHERE id <> 20;

UPDATE tbitemalarm 
SET id = id + 20000, 
    iditem = iditem + 20000 
WHERE id <> 20;

UPDATE tbitemalarm 
SET idasociado = idasociado + 20000 
WHERE idasociado <> 0;

UPDATE tbitemalarm_bc 
SET id = id + 20000, 
    idItemalarm = idItemalarm + 20000 
WHERE id <> 20;

-- Consultas de verificación
SELECT idtag, name, calculation 
FROM tbtag 
WHERE idtag IN (24020048, 24020645);

SELECT name, y.* 
FROM tbambientalvle y 
LEFT JOIN tbtag t ON t.idtag = y.idtag;

-- Reemplazo de nombres NOX → SO2
UPDATE tbtag 
SET name = REPLACE(name, 'NOX', 'SO2') 
WHERE name LIKE '%NOX%';

UPDATE tbtag 
SET description = REPLACE(description, 'NOX', 'SO2') 
WHERE description LIKE '%NOX%';

UPDATE alarmas 
SET nombre = REPLACE(nombre, 'NOX', 'SO2') 
WHERE nombre LIKE '%NOX%';

UPDATE alarmas 
SET descripcion = REPLACE(descripcion, 'NOX', 'SO2') 
WHERE descripcion LIKE '%NOX%';

UPDATE tbtag 
SET calculation = REPLACE(calculation, 'NOX', 'SO2') 
WHERE calculation LIKE '%NOX%';

-- Tags CGG
UPDATE xt_configtags 
SET id_parametro = id_parametro + 20000;
```
### Pas 3, Migrar el contaminant clonat a la bbdd principal

1. Modificar pv22_celsa_multifoco pel nom de la bbdd que rebra la update, executar desde la bbdd clonada
```SQL
-- ***** SCRIPT PARA COPIAR BD CLONADA****  
-- Supone que la condición siempre true tiene alarmas.id =20, tbitemalarm.id = 20 y tbitemalarm_bc.id = 20  
  
insert into pv22_celsa_multifoco.tbtag select * from tbtag ; --  where name not like 'CV%';  
insert into pv22_celsa_multifoco.tbcalculatetag select * from tbcalculatetag;  
insert into pv22_celsa_multifoco.alarmas select * from alarmas where id <> 20;  
insert into pv22_celsa_multifoco.tbitemalarm select * from tbitemalarm where id <> 20;  
INSERT INTO pv22_celsa_multifoco.tbitemalarm_bc
SELECT * FROM tbitemalarm_bc
WHERE id <> 20;
insert into pv22_celsa_multifoco.tbambientalvle select * from tbambientalvle;  
insert into pv22_celsa_multifoco.xt_configtags select * from xt_configtags;  
-- suponemos que el id del usuario opearador es 3  
-- select * from xt_users; # para ver que id tienen asignadas los usuarios (3 en este ejemplo)
delete from pv22_celsa_multifoco.xt_tags_permissions;  
insert into pv22_celsa_multifoco.xt_tags_permissions select null,idtag,0,null,3 From pv22_celsa_multifoco.tbtag;  
insert into pv22_celsa_multifoco.xt_tags_permissions select null,idtag,2,null,3 From pv22_celsa_multifoco.tbtag;
```