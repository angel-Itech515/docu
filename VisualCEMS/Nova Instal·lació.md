
# Activació de llicència, License.lic

PATH programa generador de llicències: "C:\ITech515\Desarrollo\PlantValue\PlantValue Tools\PlantValue License Generator\bin\Debug\PV_License Generator.exe"
Accedir Mode admin, x3 clics:
![[Pasted image 20250402114848.png]]
Accedir com a Itech515 i ficar totes les parts de license info a infinit, sobretot establir les interfaces com toca i treure data, la ID Install s'ha de fer fent click a genera.
![[Pasted image 20250402114936.png]]
![[Pasted image 20250402115130.png]]
```SQL
-- Credencials bbdd: portal.plantvalue.com / pvuser / PV99013939

SELECT * FROM jos_usergroups j where title='PVXV7395';
-- tries 2 és el màxim, ficar a 0 per resetejar
```

# Configuració bbdd

Cal revisar:

```SQL
SELECT * FROM focos f;

SELECT * FROM tbinstancia;
UPDATE tbinstancia
SET nombre = REPLACE(nombre, 'trarg', 'saica')
WHERE nombre LIKE '%trarg%';

SELECT * FROM tbitemcsv;
```


## Arregla tbparamgenerales

```sql
insert into tbparamgenerales values('RecalculationDate_Current', '2100-01-01 00:00:00'),  
('RecalculationDate_CurrentStart', '2024-07-19 22:00:00'),  
('RecalculationDate_ServerStart', '2024-09-02 08:39:41'),  
('RecalculationDate_Start', '2100-01-01 00:00:00');
```

## Arregla bits_controli

```sql
ALTER TABLE $pv22_bd.bits_controli ADD COLUMN color VARCHAR(50) AFTER ValueSubstitution;
```
