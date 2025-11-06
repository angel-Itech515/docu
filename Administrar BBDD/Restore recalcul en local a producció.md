Perfecto 👍, con esos detalles ya podemos armar el **script SQL de traspaso** claro y seguro.

---
## 📌 Contexto

- **Producción** → `pv22_saica_papelera_replica`
    
- **Backup restablecido** → `RECALCUL_SAICA_20250915`
    
- **Fecha límite de corte** → `2025-08-25 09:44:30`
    
---
## 🔹 Queries

### 1. Tablas `z_...` completas

```sql
REPLACE INTO pv22_saica_papelera_replica.z_2025
SELECT *
FROM RECALCUL_SAICA_20250915.z_2025;

REPLACE INTO pv22_saica_papelera_replica.z_2025_1
SELECT *
FROM RECALCUL_SAICA_20250915.z_2025_1;

REPLACE INTO pv22_saica_papelera_replica.z_2025_2
SELECT *
FROM RECALCUL_SAICA_20250915.z_2025_2;

REPLACE INTO pv22_saica_papelera_replica.z_2025_3
SELECT *
FROM RECALCUL_SAICA_20250915.z_2025_3;

REPLACE INTO pv22_saica_papelera_replica.z_2025_4
SELECT *
FROM RECALCUL_SAICA_20250915.z_2025_4;

REPLACE INTO pv22_saica_papelera_replica.z_2025_5
SELECT *
FROM RECALCUL_SAICA_20250915.z_2025_5;

REPLACE INTO pv22_saica_papelera_replica.z_2025_6
SELECT *
FROM RECALCUL_SAICA_20250915.z_2025_6;

REPLACE INTO pv22_saica_papelera_replica.z_2025_7
SELECT *
FROM RECALCUL_SAICA_20250915.z_2025_7;

-- Y así con todas las tablas Z que quieras restaurar
```
---
### 2. Tabla de agosto (ejemplo `z_agost`)

```sql
REPLACE INTO pv22_saica_papelera_replica.z_agost
SELECT *
FROM RECALCUL_SAICA_20250915.z_agost
WHERE dia < '2025-08-25 09:44:30';
```

---

### 3. Tabla year (`y_2025`)

⚠️ Aquí **NO usar REPLACE** para evitar totalizadores sueltos.

```sql
-- 2025-08-22 04:20:10
-- 2025-08-21 22:00:00
DELETE FROM pv22_saica_papelera_replica.y_2025
WHERE dia < '2025-08-21 22:00:00';

INSERT INTO pv22_saica_papelera_replica.y_2025 
       (dia, id_parametro, valor, valor_corregido, caracter_validacion)
SELECT dia, id_parametro, valor, valor_corregido, caracter_validacion
FROM RECALCUL_SAICA_20250915.y_2025
WHERE dia < '2025-08-21 22:00:00';
```

---

### 4. Tabla de totalizadores

```sql
REPLACE INTO pv22_saica_papelera_replica.registro_Totalizadores 
       (IdTot, RegDate, IdTag, DateBegin, DateEnd, Value, Priority, Reset, Absolute)
SELECT IdTot, RegDate, IdTag, DateBegin, DateEnd, Value, Priority, Reset, Absolute
FROM RECALCUL_SAICA_20250915.registro_Totalizadores;
```

---

### 5. (Pendiente fuera de SQL)

- **Recalcular totalizadores desde el 25 de agosto (día completo)** → esto lo tendrás que lanzar con el procedimiento o script propio de vuestro sistema.