
# MACROS EN EXCEL

Activar Macro en Excel Alt+F11

Concatenar multiples celdas seleccionadas

```vb
Function CC(Rango As Range)
    ncel = 1
    For Each celda In Rango.Cells
        
        If celda.Value <> "" Then
        
            res = res & " " & celda.Value
            
            If ncel > 2 Then
                res = res & ", " & vbCrLf
            End If
                        
        End If
        
        ncel = ncel + 1
        
        If ncel > 3 Then
            ncel = 1
        End If
        
    Next celda
    res = Left(res, Len(res) - 4)
    CC = res
End Function

'
' Funcion para buscar una cadena de texto y obtener los datos contuguos hasta encontrar una coma ','
' Forma de Uso asignar como formula Ej.
' =SS(L2;"TIPO TRAMITE:")
'
Function SS(Rango As Range, StrFind As String)

    Dim StrReturn As String
    Dim StrValue As String
    Dim PosFind As Long
    Dim LenFind As Long
    Dim PosNextComm As Long
    Dim LenRes As Long
    
        
    LenFind = Len(StrFind)
    
    For Each Cell In Rango.Cells
        
        StrValue = Cell.Value
        
        If StrValue <> "" Then
        
            PosFind = InStr(StrValue, StrFind)
            
            If PosFind > 0 Then
                ' Buscar la siguiente coma
                PosNextComm = InStr(PosFind + LenFind, StrValue, ",")
                LenRes = PosNextComm - PosFind - LenFind
                'MsgBox ("Pos:" & LenRes)
            
                StrReturn = Trim(Mid(StrValue, PosFind + LenFind, LenRes))
            Else
                StrReturn = ""
            End If
                        
        End If
        
            
    Next Cell
    
    SS = StrReturn
    
End Function


' Funcion para obtener la sigla de la Serie Documental

Function Serie(Rango As Range)

    For Each Cell In Rango.Cells
        
        StrValue = Cell.Value
        
        If StrValue = "PLANOS DE CONSTRUCCIÓN DE REGULARIZACIÓN" Then
                  
            StrReturn = "PC"
            
        End If
        
        If StrValue = "PROPIEDAD HORIZONTAL DE REGULARIZACIÓN" Then
                  
            StrReturn = "PH"
            
        End If
        
        If StrValue = "DIVISIÓN Y PARTICIPACIÓN DE REGULARIZACIÓN" Then
                  
            StrReturn = "DP"
            
        End If
        
            
    Next Cell
    
    Serie = StrReturn

End Function

Sub ConvertirFormulas()
 
    'Copiar la selección de celdas
    Selection.Copy
     
    'Pegado Especial utlizando xlPasteValues
    Selection.PasteSpecial Paste:=xlPasteValues
     
    'Salir del modo de copiado
    Application.CutCopyMode = False
 
End Sub

' Fusionar dos tipos de busquedas en una sola celda
' ej.
' =SSD(L2;"CODIGO CATASTRAL REF.:";"CÓDIGO CATASTRAL REF.:")
'
Function SSD(Rango As Range, StrFind As String, StrFindSec As String)

    Dim StrReturn As String
    Dim StrValue As String
    Dim PosFind As Long
    Dim LenFind As Long
    Dim PosNextComm As Long
    Dim LenRes As Long
    
    StrReturn = ""
    
    For Each Cell In Rango.Cells
        
        StrValue = Cell.Value
        
        If StrValue <> "" Then
            
            PosFind = InStr(StrValue, StrFind)            
            If PosFind > 0 Then
                LenFind = Len(StrFind)
                PosNextComm = InStr(PosFind + LenFind, StrValue, ",")
                LenRes = PosNextComm - PosFind - LenFind
                StrReturn = Trim(Mid(StrValue, PosFind + LenFind, LenRes))                
            End If

            PosFind = InStr(StrValue, StrFindSec)            
            If PosFind > 0 Then
                LenFind = Len(StrFindSec)
                PosNextComm = InStr(PosFind + LenFind, StrValue, ",")
                LenRes = PosNextComm - PosFind - LenFind
                StrReturn = Trim(Mid(StrValue, PosFind + LenFind, LenRes))                
            End If

        End If
    Next Cell
    
    SS = StrReturn
        
End Function

```


### FORMULAS EXCEL

```sh
=SI(K4=K3;H3&", "&E4&" "&F4&" "&G4;E4&" "&F4&" "&G4)            // copiar en segunda fila
=SI(K3<>K4;"No eliminar"; "Eliminar")                           // copiar en primera fila


=SI(M4=M3;H3&", "&E4&" "&F4&" "&G4;E4&" "&F4&" "&G4)            // copiar en segunda fila
=SI(M3<>M4;"No eliminar"; "Eliminar")                           // copiar en primera fila

// Busuqedas de Cadenas

=SI(ESNUMERO(HALLAR("NOMBRE";M2));M2;"")

```
