### Apps Script code that will allow you to append an entire row of data from one sheet to another based on a dropdown selection

* just Copy and Past Script and Change the SheetName Details

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
  if (editedSheet.getName() == sourceSheetName && editedColumn == 2) {
    var sourceSheet = e.source.getSheetByName(sourceSheetName);
    var pendingSheet = e.source.getSheetByName(pendingSheetName);
    var completedSheet = e.source.getSheetByName(completedSheetName);
    var droppedSheet = e.source.getSheetByName(droppedSheetName);
    
    var selectedRow = editedRange.getRow();
    var lastColumn = sourceSheet.getLastColumn();
    
    if (editedValue == "Pending") {
      var sourceRange = sourceSheet.getRange(selectedRow, 1, 1, lastColumn);
      var targetRange = pendingSheet.getRange(pendingSheet.getLastRow() + 1, 1, 1, lastColumn);
      sourceRange.copyTo(targetRange);
    } else if (editedValue == "Completed") {
      var sourceRange = sourceSheet.getRange(selectedRow, 1, 1, lastColumn);
      var targetRange = completedSheet.getRange(completedSheet.getLastRow() + 1, 1, 1, lastColumn);
      sourceRange.copyTo(targetRange);
    } else if (editedValue == "Dropped") {
      var sourceRange = sourceSheet.getRange(selectedRow, 1, 1, lastColumn);
      var targetRange = droppedSheet.getRange(droppedSheet.getLastRow() + 1, 1, 1, lastColumn);
      sourceRange.copyTo(targetRange);
    }
  }
}

```
