# VBA-
VBA Codes for few of the basic procedures.
Sub HideAllExceptActiveSheet()
Dim ws As Worksheet
For Each ws In ThisWorkbook.Worksheets
If ws.Name <> ActiveSheet.Name Then ws.Visible = xlSheetHidden
Next ws
End Sub

Sub UnhideAllWoksheets()
Dim ws As Worksheet
For Each ws In ActiveWorkbook.Worksheets
ws.Visible = xlSheetVisible
Next ws
End Sub

Sub SortSheetsTabName()
Application.ScreenUpdating = False
Dim ShCount As Integer, i As Integer, j As Integer
ShCount = Sheets.Count
For i = 1 To ShCount - 1
For j = i + 1 To ShCount
If Sheets(j).Name < Sheets(i).Name Then
Sheets(j).Move before:=Sheets(i)
End If
Next j
Next i
Application.ScreenUpdating = True
End Sub

Sub ProtectAllSheets()
Dim ws As Worksheet
For Each ws In Worksheets
ws.Protect ["Test123"]
Next ws
End Sub

Sub UnprotectAllSheets()
Dim ws As Worksheet
For Each ws In Worksheets
ws.Unprotect ["Test123"]
Next ws
End Sub

Sub UnhideAllHiddenRowsAndColumns()
Columns.EntireColumn.Hidden = False
Rows.EntireRow.Hidden = False
End Sub

Sub UnmergeAllCells()
For Each sht In Worksheets
    sht.Cells.UnMerge
Next sht
End Sub

Sub SaveAsFilenameWithTimestamp()
Dim xWb As Workbook
Dim xStrDate As String
Dim xFileName As Variant
Dim xFileDlg As FileDialog
Dim i As Variant
Application.DisplayAlerts = False
Set xWb = ActiveWorkbook
xStrDate = Format(Now, "yyyy-mm-dd hh-mm-ss")
If Right(xWb.Name, 4) = "xlsm" Then
  xFileName = Application.GetSaveAsFilename(xStrDate, "Excel Macro-Enabled Workbook (*.xlsm),*.xlsm")
Else
  xFileName = Application.GetSaveAsFilename(xStrDate, "Excel Workbook (*.xlsx),*.xlsx")
End If
If xFileName = False Then
Else
  xWb.SaveAs (xFileName)
End If
Application.DisplayAlerts = True
End Sub

Sub SaveEachWorksheetAsPDF()
Dim ws As Worksheet
For Each ws In Worksheets
ws.ExportAsFixedFormat xlTypePDF, " " & ws.Name & ".pdf"
Next ws
End Sub

Sub ConvertFormulasToValuesAllWorksheets()
Dim ws As Worksheet, rng As Range
For Each ws In ActiveWorkbook.Worksheets
For Each rng In ws.UsedRange
If rng.HasFormula Then
rng.Formula = rng.Value
End If
Next rng
Next ws
End Sub
