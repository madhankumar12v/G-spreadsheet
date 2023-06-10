### Data Copy to One File(Specific column) to another File(specific column)

```
function onEdit(e) {
  var sourceSheetName = "Source Sheet";
  var destinationSpreadsheetId = "Destination Spreadsheet ID";
  var destinationSheetName = "Destination Sheet";

  var activeSheet = e.source.getActiveSheet();

  // Check if the edited sheet is the source sheet
  if (activeSheet.getName() === sourceSheetName) {
    var editedRange = e.range;
    var editedColumn = editedRange.getColumn();

    // Specify the mapping of source and destination columns
    var columnMapping = {
      1: 2,  // Source column 1 moves to destination column 2
      3: 3,  // Source column 3 moves to destination column 3
      5: 5   // Source column 5 moves to destination column 5
    };

    var sourceColumns = Object.keys(columnMapping).map(Number);

    // Check if the edited column is in the source columns
    if (sourceColumns.includes(editedColumn)) {
      var sourceValues = activeSheet.getDataRange().getValues();

      // Open the destination spreadsheet
      var destinationSpreadsheet = SpreadsheetApp.openById(destinationSpreadsheetId);

      // Select the destination sheet
      var destinationSheet = destinationSpreadsheet.getSheetByName(destinationSheetName);

      // Clear the existing data in the destination sheet for the corresponding column
      var destinationColumn = columnMapping[editedColumn];
      destinationSheet.getRange(1, destinationColumn, destinationSheet.getLastRow(), 1).clearContent();

      // Move the values from the source sheet to the destination sheet for the corresponding column
      for (var i = 0; i < sourceValues.length; i++) {
        var sourceColumn = editedColumn;
        var destinationValue = sourceValues[i][sourceColumn - 1];
        destinationSheet.getRange(i + 1, destinationColumn).setValue(destinationValue);
      }
    }
  }
}


```
