### To automatically append rows to another sheet in Google Sheets when a checkbox is ticked, you can use Google Apps Script. Here's a step-by-step guide to setting it up:

* Open your Google Sheets document.

* If you want to move the data to the next available row in Sheet2 (starting from row 1 to 87) when there is existing data, you can modify the code as follows

* Create a new sheet to store the appended rows. For this example, let's name it "Appended Data."

* In the menu bar, click on "Extensions" and select "Apps Script" to open the Apps Script editor.

* In the Apps Script editor, delete any existing code and replace it with the following code:



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

      var sourceSelectedColumns = [1, 2, 4, 6, 9, 11, 12]; // Specify the source selected column numbers
      var targetSelectedColumns = [1, 3, 5, 6, 8, 9, 12]; // Specify the target selected column numbers

      // Find the next available row in Sheet2
      var targetRow = 1;
      while (targetSheet.getRange(targetRow, 1).getValue() != "" && targetRow < 88) {
        targetRow++;
      }

      // Move the data to the next available row in Sheet2
      for (var i = 0; i < sourceSelectedColumns.length; i++) {
        var sourceColumn = sourceSelectedColumns[i];
        var targetColumn = targetSelectedColumns[i];
        targetSheet.getRange(targetRow, targetColumn).setValue(sourceData[sourceColumn - 1]);
      }

      // Delete the ticked row
      sourceSheet.deleteRow(row);
    }
  }
}

```

* In the above script, you need to specify the desired column numbers in the selectedColumns array. For example, if you want to transfer data from columns A, C, and E, you would set selectedColumns to [1, 3, 5].

* The script extracts the values from the specified columns for the edited row and appends them to the target sheet. The ticked row is then deleted from the source sheet.

* Remember to set up the installable trigger as explained in the previous response to activate the onEdit function.
