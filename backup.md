* To transfer the exact data from Sheet1 to Sheet2 without overwriting the existing data in Sheet2, you can use the following script:

```
function onEdit(e) {
  var sourceSheetName = "Backup";  // Replace with the name of your source sheet
  var targetSheetName = "Sheet4";  // Replace with the name of your target sheet

  var sheet = e.source.getSheetByName(sourceSheetName);
  var targetSheet = e.source.getSheetByName(targetSheetName);

  if (sheet.getName() === sourceSheetName) {
    var sourceRange = sheet.getDataRange();
    var sourceData = sourceRange.getValues();
    
    var targetRange = targetSheet.getRange(1, 1, sourceRange.getNumRows(), sourceRange.getNumColumns());
    targetRange.setValues(sourceData);
  }
}

```
