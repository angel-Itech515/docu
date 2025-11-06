**Comparació entre CALCHOWMANYTIMES i CALCCOUNT (via callValoresProcesadosExt) en PlantValue**

Aquesta documentació té com a objectiu explicar les diferències entre dues funcions utilitzades dins l'entorn PlantValue: `CALCHOWMANYTIMES(...)` i `CALCCOUNT(...)` (que delega en `callValoresProcesadosExt(...)`). Tot i compartir certa lògica i components comuns, aquestes funcions tenen finalitats i comportaments molt diferents.

---

## 1. Funcions comparades

### 1.1. `CALCHOWMANYTIMES(string fechaIni, string fechaFin, string condicion)`

- **Objectiu**: Comptar quantes vegades una condició és certa dins un rang de dates.
    
- **Mètode intern**: `PlantValueCoreLibrary.Excel.ContarVeces(...)`
    
- **Entrada principal**: `condicion` (expressió lògica com ara `['TAG'] > 5`)
    
- **Sortida**: Un nombre enter (quantes vegades s'ha complert la condició)
    
- **Requereix nom de tag?** No explícitament (el tag s'inclou dins la condició)
    

> **Nota**: Aquesta funció és una crida directa a CALCHOWMANYTIMES.

```vb
PARAM = "CO-STATUS.DPN" 
FOCO = "FOCO-STATUS.DPN" 
MEDIA = "CO-STATUS-60MIN" 
COMBUSTIBLE = "FOCO-COMBUSTIBLE.DPN" 
VALORCOM = 2 ' Valor del combustible (1 para s1, 2 para s2,...)

FILTER_NN = "([" & FOCO & "]=0 OR [" & FOCO & "]=4) AND [" & COMBUSTIBLE & "]=" & VALORCOM 
FILTER_RV = "([" & FOCO & "]=0 OR [" & FOCO & "]=4) AND [" & COMBUSTIBLE & "]=" & VALORCOM & " AND [" & PARAM & "]>=8"

numMediasTotales = CInt(CALCHOWMANYTIMES("BEGINUTC", "ENDUTC", FILTER_NN))
```

---

### 1.2. `CALCCOUNT(string sTags, string fechaIni, string fechaFin, string sFiltro)`

- **Objectiu**: Comptar el nombre de valors vàlids d’un tag dins un rang de dates.
    
- **Mètode intern**: `callValoresProcesadosExt(...)`
    
- **Paràmetres interns**: Usa `operation = 6`, que indica "comptador"
    
- **Requereix nom de tag?** Sí (via `sTags`)
    

```csharp
public double CALCCOUNT(string sTags, string fechaIni, string fechaFin, string sFiltro)
{
    int operation = 6;
    return callValoresProcesadosExt(sTags, fechaIni, fechaFin, sFiltro, operation, "CALCCOUNT", "1", false);
}
```

> Aquesta funció utilitza `callValoresProcesadosExt` amb operació 6 per obtenir el comptador de valors vàlids.

```csharp
PARAM = "CO-STATUS.DPN" 
FOCO = "FOCO-STATUS.DPN" 
MEDIA = "CO-STATUS-60MIN" 

FILTER_NN = "[" & FOCO & "]=0 OR [" & FOCO & "]=4" 
FILTER_RV = "[" & PARAM & "]>=8" 

numMediasTotales = CInt(CALCCOUNT(FOCO,'BEGINUTC','ENDUTC',FILTER_NN))
```

---

## 2. Resum comparatiu

|Aspecte|`CALCHOWMANYTIMES`|`CALCCOUNT` (via `callValoresProcesadosExt`)|
|---|---|---|
|**Funció principal**|Comptar ocurrències d'una condició|Comptar valors vàlids d’un tag|
|**Mètode PlantValue usat**|`ContarVeces`|`ValoresProcesadosUnTag`|
|**Input principal**|`condicion` (expressió lògica)|`sTags`, `sFiltro`|
|**Tipus de sortida**|Nombre enter (comptador)|Nombre enter (comptador)|
|**Requereix tag explícit?**|No|Sí|

---
## 3. Conclusió

Utilitza:

- `CALCHOWMANYTIMES` quan necessites saber **quantes vegades** una condició s'ha donat (sense centrar-te en un tag concret).
    
- `CALCCOUNT` quan vols comptar **quants valors vàlids** ha tingut un **tag específic**.
    

Totes dues funcions són complementàries i poden combinar-se en anàlisis més complexes dins del sistema PlantValue.