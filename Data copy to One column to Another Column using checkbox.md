### Data copy to One column to Another Column using checkbox


```
function onEdit1(e) {
  var sheet = e.source.getActiveSheet();
  var editedCell = e.range;
  
  if (editedCell.getA1Notation() === "J2" && editedCell.isChecked()) {
    var sourceRange = sheet.getRange("F2:F1000");
    var sourceValues = sourceRange.getValues();
    var targetRange = sheet.getRange("G2:G1000");
    targetRange.setValues(sourceValues);

    SpreadsheetApp.getActiveSpreadsheet().toast("Data copied!", "Success", 3);
  }
}


```
