### To automatically create a "Today" column in Google Sheets, you can use a formula or a script

* Just copy and paste the script and change to the desired column Number
```
function onEdit4(e) {
  var sheet = e.source.getActiveSheet();
  var editedCell = e.range;
  var dataColumn = 2; // Change to the desired data column number
  var dateColumn = 1; // Change to the desired date column number

  if (editedCell.getColumn() === dataColumn && sheet.getName() === "Tracker") { // Modify "Sheet1" to your sheet's name
    var row = editedCell.getRow();
    var dateCell = sheet.getRange(row, dateColumn);
    var currentDate = Utilities.formatDate(new Date(), Session.getScriptTimeZone(), "dd-MMM-yyyy");
    dateCell.setValue(currentDate);
  }
}

```
