```SQL
CREATE SCHEMA $NAME_BD;

-- Opcional, pot solventar errors al fer el create
set global innodb_strict_mode=OFF;

C:\Xampp\MySQL\bin\mysql -u pvuser -pPV99013939 $NAME_BD < "C:\Users\Proacit\Desktop\20250123-114405-$NAME_BD-STRUCT.sql"
C:\Xampp\MySQL\bin\mysql -u pvuser -pPV99013939 $NAME_BD < "C:\Users\Proacit\Desktop\20250123-114405-$NAME_BD-CONFIG.sql"
C:\Xampp\MySQL\bin\mysql -u pvuser -pPV99013939 $NAME_BD < "C:\Users\Proacit\Desktop\20250123-114405-$NAME_BD-SCREENS.sql"
```
