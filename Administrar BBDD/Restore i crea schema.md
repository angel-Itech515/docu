```SQL
CREATE SCHEMA $NAME_BD;

-- Opcional, pot solventar errors al fer el create
set global innodb_strict_mode=OFF;

C:\Xampp\MySQL\bin\mysql -u pvuser -pPV99013939 $NAME_BD < "C:\Users\Proacit\Desktop\20250123-114405-$NAME_BD-STRUCT.sql"
C:\Xampp\MySQL\bin\mysql -u pvuser -pPV99013939 $NAME_BD < "C:\Users\Proacit\Desktop\20250123-114405-$NAME_BD-CONFIG.sql"
C:\Xampp\MySQL\bin\mysql -u pvuser -pPV99013939 $NAME_BD < "C:\Users\Proacit\Desktop\20250123-114405-$NAME_BD-SCREENS.sql"
```

# Restore i Backup .mysql

## Taules individuals

#### Backup
```
c:\xampp\mysql\bin\mysqldump  --password=PV99013939 --user=pvuser --quick --add-drop-table --add-locks --extended-insert --single-transaction --routines --triggers --force -C  pv22_ursa_f21 z_2025_7 > 
c:\itech515\wrk\AngelMigracio\pv22_ursa_f21_z_2025_7.sql

c:\xampp\mysql\bin\mysqldump -h 127.0.0.1 -u pvuser -pPV99013939 --quick --add-drop-table --add-locks --extended-insert --single-transaction --routines --triggers --force -C pv22_saica_papelera_replica z_2025_3 > test.sql
```
#### Restore
```
C:\xampp\mysql\bin\mysql -u pvuser -pPV99013939 emisiones < "C:\Users\Itech515\Desktop\emisiones20250809.sql"
```
# Restore i backup PlantValue (usant tool pròpia)
```

"D:\ITech515\Core\PlantValue - Backup\PV_Backup.exe"
"D:\ITech515\Core\PlantValue - Backup\PV_Restore.exe"

PV_Restore.exe "C:\PVBACKUP\RESTORE\SIRUSA" /database=rt19_sirusa_linea1 /histables=yes /setall=yes /structure=yes

"D:\ITech515\Core\PlantValue - Backup\PV_Restore.exe" "D:\Itech515_Data SSD\Backups\full\pv22_ursa_f21" /database=pv22_ursa_f21 /histables=yes /setall=yes /structure=yes
```

