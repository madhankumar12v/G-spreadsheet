### Apps Script code that will allow you to append an entire row of data from one sheet to another based on a dropdown selection

*Just Copy and Past Script and Change the SheetName Details

```
function onEdit(e) {
  var sourceSheetName = "Sheet1"; // Replace with the name of your source sheet
  var pendingSheetName = "Pending"; // Replace with the name of your pending sheet
  var completedSheetName = "Completed"; // Replace with the name of your completed sheet
  var droppedSheetName = "Dropped"; // Replace with the name of your dropped sheet
  
  var editedSheet = e.source.getActiveSheet();
  var editedRange = e.range;
  var editedValue = e.value;
  var editedColumn = editedRange.getColumn();
  
  // Check if the edit was made in the dropdown column
  if (editedSheet.getName() == sourceSheetName && editedColumn == 16) {
    var sourceSheet = e.source.getSheetByName(sourceSheetName);
    var pendingSheet = e.source.getSheetByName(pendingSheetName);
    var completedSheet = e.source.getSheetByName(completedSheetName);
    var droppedSheet = e.source.getSheetByName(droppedSheetName);
    
    var selectedRow = editedRange.getRow();
    var lastColumn = sourceSheet.getLastColumn();
    var rowData = sourceSheet.getRange(selectedRow, 1, 1, lastColumn).getValues()[0];
    
    if (editedValue == "Pending") {
      pendingSheet.appendRow(rowData);
      sourceSheet.deleteRow(selectedRow);
    } else if (editedValue == "Completed") {
      completedSheet.appendRow(rowData);
      sourceSheet.deleteRow(selectedRow);
    } else if (editedValue == "Dropped") {
      droppedSheet.appendRow(rowData);
      sourceSheet.deleteRow(selectedRow);
    }
  }
}

```
