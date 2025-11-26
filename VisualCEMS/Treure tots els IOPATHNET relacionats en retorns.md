```SQL
SELECT 'FA' AS db, name, iopathnet  
FROM pv22_rq_f10_ett.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'FB', name, iopathnet  
FROM pv22_rq_f11_acn_2025.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'EI', name, iopathnet  
FROM pv22_rq_f12_cg1.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'EN', name, iopathnet  
FROM pv22_rq_f13_regenox.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'EJ', name, iopathnet  
FROM pv22_rq_f15_crc1.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'EK', name, iopathnet  
FROM pv22_rq_f16_crc2.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'EL', name, iopathnet  
FROM pv22_rq_f17_cvc.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'EO', name, iopathnet  
FROM pv22_rq_f19_poliflex.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'EP', name, iopathnet  
FROM pv22_rq_f20_polipoli.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'f45_rtoopsm', name, iopathnet  
FROM pv22_rq_f45_rtoopsm.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'X3', name, iopathnet  
FROM pv22_rq_tx_acn.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'X2', name, iopathnet  
FROM pv22_rq_tx_bn.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'EM', name, iopathnet  
FROM pv22_rq_tx_opsm.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'X4', name, iopathnet  
FROM pv22_rq_tx_pead.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet  
  
UNION ALL  
SELECT 'X1', name, iopathnet  
FROM pv22_rq_tx_pp.tbtag  
WHERE selected = 1 AND iopathnet <> '' AND property1 = 'W' group by iopathnet;
```