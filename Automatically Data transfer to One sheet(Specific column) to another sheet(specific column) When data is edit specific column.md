### If you enter data in Column B, it will copy the corresponding data from Column A and B to Target sheet


```
function onEdit(e) {
  var sourceSheetName = "SourceSheet";
  var targetSheetName = "TargetSheet";
  var sourceColumnA = 1; // Column A
  var sourceColumnB = 2; // Column B
  var targetColumnA = 1; // Target Column A
  var targetColumnB = 2; // Target Column B
  
  var sheet = e.source.getActiveSheet();
  
  // Check if the edited column is B and there's a value in that cell
  if (sheet.getName() === sourceSheetName && e.range.getColumn() === sourceColumnB && e.value) {
    var valueA = sheet.getRange(e.range.getRow(), sourceColumnA).getValue();
    var valueB = e.value;
    
    // Open the target sheet
    var targetSheet = e.source.getSheetByName(targetSheetName);
    
    // Append data to the target sheet
    targetSheet.appendRow([valueA, valueB]);
    
    // Show a message to the user
    SpreadsheetApp.getUi().alert('Data copied to ' + targetSheetName + '.');
    
    // Optionally, you can set values in specific target columns
    targetSheet.getRange(targetSheet.getLastRow(), targetColumnA).setValue(valueA);
    targetSheet.getRange(targetSheet.getLastRow(), targetColumnB).setValue(valueB);
  }
}

```
