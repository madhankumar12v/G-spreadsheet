



```
function onEdit(e) {
  var sourceSheet = e.source.getActiveSheet();
  var targetSheet = e.source.getSheetByName("Sheet2");
  var range = e.range;

  // Check if the edited cell is in the desired column (e.g., column A for the checkbox)
  if (range.getColumn() == 6) {
    // Check if the edited cell is checked
    if (range.isChecked()) {
      var row = range.getRow();
      var lastColumn = sourceSheet.getLastColumn();
      var sourceData = sourceSheet.getRange(row, 1, 1, lastColumn).getValues()[0];

      var targetData = [];
      var selectedColumns = [1, 3, 5]; // Specify the desired column numbers (e.g., 1, 3, 5)

      // Loop through the selected columns and extract the corresponding data
      for (var i = 0; i < selectedColumns.length; i++) {
        var column = selectedColumns[i];
        targetData.push(sourceData[column - 1]);
      }

      // Append the selected data to the "Moved Data" sheet
      targetSheet.appendRow(targetData);

      // Delete the ticked row
      sourceSheet.deleteRow(row);
    }
  }
}


```
