Al fer canvis d'any pot ser que les taules del visualCEMS/Plantvalue es referenciin malament dinàmicament degut a un bug de la taula xt_configuration.

Cal seguir tres passos:
1. Eliminar els camps en un PATH cap al xampp de la taula xt_configuration
![[Pasted image 20260115101029.png]]
2. Apagar tots els serveis excepte les IF de lectura
3. Modificar el nom mal registrats tant dins de xt_histexttables com xt_historicaltables (p.ex. C/XAMPP/TABLE/y_2026 a y_2026)
4. Fer un alter name de la taula year mal generada al nom que toca (p.ex. C/XAMPP/TABLE/y_2026 a y_2026)
5. Reiniciar serveis i revisar logs

```SQL
SELECT * FROM xt_configuration x;
SELECT * FROM xt_histexttables x;
SELECT * FROM xt_historicaltables x;
```
