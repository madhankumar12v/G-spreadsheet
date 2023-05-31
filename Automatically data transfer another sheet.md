### To transfer the exact data from Sheet1 to Sheet2 without overwriting the existing data in Sheet2, you can use the following script:

* Open your Google Sheets document.
* Click on "Extensions" in the top menu and select "Apps Script" to open the script editor.
* Replace any existing code in the script editor with the following code:

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
* Replace "Sheet1" with the name of your source sheet and "Sheet2" with the name of your target sheet. Make sure to keep the names in quotes ("").
* Save the script by clicking on the floppy disk icon or pressing Ctrl + S.
* Close the script editor.
* Now, whenever you enter text in the first column of the source sheet, it will automatically be transferred to the target sheet.
