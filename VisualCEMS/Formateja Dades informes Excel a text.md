```Visual Basic
Sub ConvertirFormulasAValores()
    Dim ws As Worksheet
    Dim celda As Range
    
    ' Desactivar actualizaciones para mayor rapidez
    Application.ScreenUpdating = False
    Application.Calculation = xlCalculationManual
    
    ' Recorrer todas las hojas del libro activo
    For Each ws In ActiveWorkbook.Sheets
        ' Seleccionar todas las celdas con datos
        On Error Resume Next
        Set celda = ws.UsedRange
        If Not celda Is Nothing Then
            ' Copiar y pegar valores manteniendo formato
            celda.Copy
            celda.PasteSpecial Paste:=xlPasteValuesAndNumberFormats
            Application.CutCopyMode = False
        End If
        On Error GoTo 0
    Next ws
    
    ' Restaurar configuración de Excel
    Application.Calculation = xlCalculationAutomatic
    Application.ScreenUpdating = True
    
    MsgBox "Todas las fórmulas han sido convertidas a valores, manteniendo el formato.", vbInformation, "Proceso completado"
End Sub
```

```
# Cal declarar-lo com:
Call ConvertirFormulasAValores
```

Excel xslm (compatibilitat per a macros)
Cal fer alt+F11
Insertar -> Módulo

Executa el Alt+F8

ExcelComplement(alt+f11): Noesproacit20110101