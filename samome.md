

```
function onEdit(e) {
  var sourceSheetName = "Backup";  // Replace with the name of your source sheet
  var targetSheetName = "Sheet4";  // Replace with the name of your target sheet

  var sourceColumnsToMove = [1, 3, 5];  // Specify the source columns to be moved
  var targetColumnsToMove = [2, 3, 5];  // Specify the corresponding target columns

  var sheet = e.source.getSheetByName(sourceSheetName);
  var targetSheet = e.source.getSheetByName(targetSheetName);

  if (sheet.getName() === sourceSheetName) {
    var sourceRange = sheet.getDataRange();
    var sourceData = sourceRange.getValues();

    var targetData = [];
    for (var i = 0; i < sourceData.length; i++) {
      var rowData = [];
      for (var j = 0; j < sourceColumnsToMove.length; j++) {
        var sourceColumnIndex = sourceColumnsToMove[j] - 1;
        var targetColumnIndex = targetColumnsToMove[j] - 1;
        rowData[targetColumnIndex] = sourceData[i][sourceColumnIndex];
      }
      targetData.push(rowData);
    }

    var targetRange = targetSheet.getRange(1, 1, targetData.length, targetData[0].length);
    targetRange.setValues(targetData);
  }
}

```
