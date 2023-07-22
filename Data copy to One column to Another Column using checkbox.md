### Data copy to One column to Another Column using checkbox


```
function onEdit(e) {
  var sheetName = "Sheet1"; // Replace "Sheet1" with the name of your target sheet
  var dataColumn = "B"; // Column name where data is entered
  var todayColumn = "A"; // Column name where "Today" values will be inserted

  var sheet = e.source.getSheetByName(sheetName);
  var range = e.range;

  // Check if the edited cell is in the specified data column
  if (sheet && range.getColumn() === sheet.getRange(dataColumn + "1").getColumn()) {
    // Get the row number of the edited cell
    var row = range.getRow();

    // Get the current value of the corresponding cell in the "Today" column
    var todayCellValue = sheet.getRange(todayColumn + row).getValue();

    // Check if the cell is empty (no date exists) before updating
    if (!todayCellValue) {
      // Prepare the "Today" value to be inserted
      var todayValue = [[new Date()]];

      // Get the range of the corresponding cell in the "Today" column and set the value
      var todayRange = sheet.getRange(todayColumn + row);
      todayRange.setValue(todayValue[0][0]);

      // Show a popup alert to indicate that the "Today" value has been updated
      SpreadsheetApp.getActiveSpreadsheet().toast("Date Created!", "Success", 3);
    }
  }
}
```
