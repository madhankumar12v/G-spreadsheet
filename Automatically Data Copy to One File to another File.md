### Apps Script code snippet that copies data from one Google Sheet file to another when you enter text, and appends the data to the destination sheet.

* Here's an example of how you can achieve this:

```
function onEdit(e) {
  var sourceSheetName = "Source Sheet";
  var destinationSpreadsheetId = "Destination Spreadsheet ID";
  var destinationSheetName = "Destination Sheet";

  var activeSheet = e.source.getActiveSheet();

  // Check if the edited sheet is the source sheet
  if (activeSheet.getName() === sourceSheetName) {
    var sourceValues = activeSheet.getDataRange().getValues();

    // Open the destination spreadsheet
    var destinationSpreadsheet = SpreadsheetApp.openById(destinationSpreadsheetId);

    // Select the destination sheet
    var destinationSheet = destinationSpreadsheet.getSheetByName(destinationSheetName);

    // Clear the existing data in the destination sheet
    destinationSheet.clearContents();

    // Set the values from the source sheet to the destination sheet
    destinationSheet.getRange(1, 1, sourceValues.length, sourceValues[0].length).setValues(sourceValues);
  }
}


```

* Open the Google Sheets file where you want to run the script.
* Click on "Extensions" in the menu and select "Apps Script".
* In the Apps Script editor, you can either create a new script or modify an existing one.
* Paste the desired code into the editor.
* Save the script by clicking on the floppy disk icon or pressing Ctrl + S (Windows) or Cmd + S (Mac).
* Close the Apps Script editor.
* Go back to your Google Sheets file and refresh the page.
* Once the script is saved, it will automatically be triggered based on the specified conditions. In the provided code examples, the onEdit(e) function is triggered whenever an edit is made to the specified source sheet.
