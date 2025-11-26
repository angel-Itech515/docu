```SQL
SELECT 'FA' AS db, name, iopath  
FROM pv22_rq_f10_ett.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'FB', name, iopath  
FROM pv22_rq_f11_acn_2025.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'EI', name, iopath  
FROM pv22_rq_f12_cg1.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'EN', name, iopath  
FROM pv22_rq_f13_regenox.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'EJ', name, iopath  
FROM pv22_rq_f15_crc1.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'EK', name, iopath  
FROM pv22_rq_f16_crc2.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'EL', name, iopath  
FROM pv22_rq_f17_cvc.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'EO', name, iopath  
FROM pv22_rq_f19_poliflex.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'EP', name, iopath  
FROM pv22_rq_f20_polipoli.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'f45_rtoopsm', name, iopath  
FROM pv22_rq_f45_rtoopsm.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'X3', name, iopath  
FROM pv22_rq_tx_acn.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'X2', name, iopath  
FROM pv22_rq_tx_bn.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'EM', name, iopath  
FROM pv22_rq_tx_opsm.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'X4', name, iopath  
FROM pv22_rq_tx_pead.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%'  
  
UNION ALL  
SELECT 'X1', name, iopath  
FROM pv22_rq_tx_pp.tbtag  
WHERE selected = 1 AND iopath <> '' AND interface = 'DATOS' and name not like '%.OUT' and calculation not like '%PVCODE.RAW=%' and calculation not like '%PVCODE.VAL=%' and calculation not like '%R_V=%' and name not like '%-CALFUNC.FALLO' and calculation not like '%R=%' and calculation not like '%V=%';
```

