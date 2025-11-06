[[Queries VC]]

```SQL
select * from tbtag where idtag = 2 OR idtag = 4;
select * from tbtag where name like '%%';
select idtag,name,iopath,iopathnet,selected,calculation,flow from tbtag where name like '%%';
```
### Iopath per a les plantilles d'incorporació
```SQL
SELECT GROUP_CONCAT(name SEPARATOR ', ') AS tag_names, name, iopath, GROUP_CONCAT(idtag SEPARATOR ',') AS idtags
FROM tbtag
WHERE iopath LIKE '%'
AND interface='DATOS'
AND selected = 1
GROUP BY iopath
ORDER BY iopath;
```
### Insert de tags a partir d'altres
```SQL
-- INSERT INTO tbtag (
    Type, Itype, Otype, Name, IdFoco, Interface, Description, MaxRange, MinRange, MaxRangeOut, MinRangeOut,
    Units, Unitscustom, Conversion, MinIn, MaxIn, MinOut, MaxOut, CorrectionA, CorrectionB, Rate, RateSync,
    IOPath, IOPathNet, ExcepValue, ExcepMaxTime, Compfactorvalue, CompMaxTime, PropWrite, PropRead, ValueWrite,
    ValueRead, Selected, ValidationCode, Error, CreDate, CreUser, ModDate, ModUser, ReadingType, IdManual,
    Historical, ValueDefault, FieldGap, Flow, OutPutTags, OverwriteRaw, Calculation, Property1, Property2,
    Property3, Property4, Property5, Property6, Property7, Property8, Property9, Property10, MinValidRange,
    MaxValidRange, Area, Decimals, Step, Alias
)
SELECT
    Type, Itype, Otype,
    REPLACE(Name, 'MCS100FT', 'FW101') AS Name,
    IdFoco, Interface,
    REPLACE(Description, 'MCS100FT', 'FW101') AS Description,
    MaxRange, MinRange, MaxRangeOut, MinRangeOut, Units, Unitscustom, Conversion, MinIn, MaxIn,
    MinOut, MaxOut, CorrectionA, CorrectionB, Rate, RateSync, IOPath, IOPathNet, ExcepValue,
    ExcepMaxTime, Compfactorvalue, CompMaxTime, PropWrite, PropRead, ValueWrite, ValueRead,
    Selected, ValidationCode, Error, CreDate, CreUser, ModDate, ModUser, ReadingType, IdManual,
    Historical, ValueDefault, FieldGap, Flow, OutPutTags, OverwriteRaw, Calculation, Property1,
    Property2, Property3, Property4, Property5, Property6, Property7, Property8, Property9,
    Property10, MinValidRange, MaxValidRange, Area, Decimals, Step, Alias
FROM tbtag
WHERE Name IN ('MCS100FT_RED_MANT.IN', 'MCS100FT_RED_ERROR.IN');

-- CAS 2
-- INSERT INTO tbtag (
    Type, Itype, Otype, Name, IdFoco, Interface, Description, MaxRange, MinRange, MaxRangeOut, MinRangeOut,
    Units, Unitscustom, Conversion, MinIn, MaxIn, MinOut, MaxOut, CorrectionA, CorrectionB, Rate, RateSync,
    IOPath, IOPathNet, ExcepValue, ExcepMaxTime, Compfactorvalue, CompMaxTime, PropWrite, PropRead, ValueWrite,
    ValueRead, Selected, ValidationCode, Error, CreDate, CreUser, ModDate, ModUser, ReadingType, IdManual,
    Historical, ValueDefault, FieldGap, Flow, OutPutTags, OverwriteRaw, Calculation, Property1, Property2,
    Property3, Property4, Property5, Property6, Property7, Property8, Property9, Property10, MinValidRange,
    MaxValidRange, Area, Decimals, Step, Alias
)
SELECT
    Type, Itype, Otype,
    'H2-ACTIVADO.IN' AS Name,
    IdFoco, Interface,
    'Alarma sistema detección de H2 activado' AS Description,
    MaxRange, MinRange, MaxRangeOut, MinRangeOut, Units, Unitscustom, Conversion, MinIn, MaxIn,
    MinOut, MaxOut, CorrectionA, CorrectionB, Rate, RateSync, IOPath, IOPathNet, ExcepValue,
    ExcepMaxTime, Compfactorvalue, CompMaxTime, PropWrite, PropRead, ValueWrite, ValueRead,
    Selected, ValidationCode, Error, CreDate, CreUser, ModDate, ModUser, ReadingType, IdManual,
    Historical, ValueDefault, FieldGap, Flow, OutPutTags, OverwriteRaw, Calculation, Property1,
    Property2, Property3, Property4, Property5, Property6, Property7, Property8, Property9,
    Property10, MinValidRange, MaxValidRange, Area, Decimals, Step, Alias
FROM tbtag
WHERE Name IN ('D-Q-T-P-ERROR.IN');
```
### Columnes tbtag WHERE interface = 'DATOS'
```txt
// *** TAGS de escritura + campo TYPE (Tipo de Datos)
// Property1 = W
// Iopath = TagName a leer (idtag en DB) ( se pueden utilizar los rsystag )
// IopathNET = OPC Tag de ESCRITURA
// OType = indica el valor a devolver, RAW,VAL, CV, FORMATO, DATE según el enum Definitions.TIPO_VALOR_ESCRITURA { bruto = 0, corregido = 1, cv = 2, formato = 3, dia = 4 };
// TYPE
//          0, 'bit'
//          1, 'byte'
//          2, 'int16'
//          3, 'int32'
//          4, 'ubyte'
//          5, 'uint16'
//          6, 'uint32'
//          7, 'float32'
//          8, 'float64'
//          9, 'state'  - ('digital')
//          10, 'string'
```
### Columnes tbtag WHERE interface = 'VC'
```txt
// rate = [1...n] (min,h,dia,mes)
// Property1 = 0 min, 1 h, 2 dies, 4 mes
// Property4 = 2024/12/31 23:00:00 (defineix inici dels calculs, si vols mitjanes setmanals, cal posar-ho un dilluns per a que el rate de 7 dies "encaixi")
// Iopath = tag o senyal que actua com a trigger
// OType = indica el valor a devolver, RAW,VAL, CV, FORMATO, DATE según el enum Definitions.TIPO_VALOR_ESCRITURA { bruto = 0, corregido = 1, cv = 2, formato = 3, dia = 4 };
// TYPE
//          0, 'bit'
//          1, 'byte'
//          2, 'int16'
//          3, 'int32'
//          4, 'ubyte'
//          5, 'uint16'
//          6, 'uint32'
//          7, 'float32'
//          8, 'float64'
//          9, 'state'  - ('digital')
//          10, 'string'
```
