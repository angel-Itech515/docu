```sql
INSERT IGNORE INTO xt_configtags (dia, id_parametro, valor, valor_corregido, caracter_validacion)
VALUES
    ('2020-12-31 23:00:00', 24031430, 240, 240, 'V');

select t.name,x.* from xt_configtags x left join tbtag t on idtag=id_parametro where name like '%%';
select * from xt_configtags where id_parametro in(select idtag from tbtag where name like '%%');
```
