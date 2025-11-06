```Visual Basic
Option Explicit
Dim bInternal As Boolean
Dim bToserver As Boolean
Dim bToUser As Boolean

Private Sub Worksheet_Change(ByVal Target As Range)
    If Not bInternal Then
        bInternal = True
        
        Select Case True
            Case Not Application.Intersect(Target, Range("$C$7")) Is Nothing
                If Range("$C$7").Text = "server" Then
                    bToserver = True
                Else
                    bToUser = True
                End If
                
            Case Not Application.Intersect(Target, Range("$C$8")) Is Nothing
                If Range("$C$8").Text = "server" Then
                    bToserver = True
                ElseIf Range("$C$7").Value = "server" Then
                    bToserver = True
                End If
                
            Case Not Application.Intersect(Target, Range("$C$9")) Is Nothing
                If Range("$C$9").Text = "server" Then
                    bToserver = True
                ElseIf Range("$C$7").Value = "server" Then
                    bToserver = True
                End If
        End Select
        
        If bToUser Then
            Range("$C$8").Value = Range("$C$7").Value
            Range("$C$9").Value = Range("$C$7").Value
        ElseIf bToserver Then
            Range("$C$7").Value = "server"
            Range("$C$8").Value = "server"
            Range("$C$9").Value = "server"
        End If
        
        bInternal = False
        bToUser = False
        bToserver = False
    End If
    
    ' Llamar a la macro de conversión
    ConvertirFormulasAValores_Hoja2
End Sub

Sub ConvertirFormulasAValores_Hoja2()
    Dim celda As Range
    Dim ws As Worksheet
    
    Set ws = ThisWorkbook.Sheets("Hoja2")
    
    If Application.WorksheetFunction.CountA(ws.Cells) = 0 Then Exit Sub ' Salir si está vacía
    
    Application.ScreenUpdating = False
    Application.Calculation = xlCalculationManual
    Application.EnableEvents = False
    
    Set celda = ws.UsedRange
    celda.Copy
    celda.PasteSpecial Paste:=xlPasteValuesAndNumberFormats
    Application.CutCopyMode = False
    
    Application.EnableEvents = True
    Application.Calculation = xlCalculationAutomatic
    Application.ScreenUpdating = True
End Sub
```

CAL NOTAR que només afecta a la Hoja2, este montatge funciona perfecte a salamanca i es fa a partir del sample report.

Excel xslm (compatibilitat per a macros)
Cal fer alt+F11
Insertar -> Módulo

Executa el Alt+F8

ExcelComplement(alt+f11): Noesproacit20110101