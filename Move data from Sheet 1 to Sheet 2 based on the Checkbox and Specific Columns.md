### To move data from Sheet 1 to Sheet 2 based on the Registration Number (Reg No) and copy specific columns and paste specific columns, you can use Google Apps Script. 
### Here's an example script that accomplishes this:

```
function onEdit(e) {
  var sheet1Name = "Sheet1";
  var sheet2Name = "Sheet2";
  var checkboxColumn = 10; // Column A
  var regNoColumnSheet1 = 12; // Column B in Sheet1
  var regNoColumnSheet2 = 1; // Column A in Sheet2
  var sourceColumnsSheet1 = [13, 14, 15, 16, 17, 18, 19, 20, 21, 22,23]; // Columns M, N, O, P, Q, R, S, T, U, V in Sheet1
  var destColumnsSheet2 = [35, 36, 41, 42, 52, 59, 55, 62, 19, 20,16]; // Columns AI, AJ, AO, AP, AZ, BG, BC, BJ, S, T in Sheet2

  var range = e.range;
  var sheet = range.getSheet();

  if (sheet.getName() === sheet1Name && range.getColumn() === checkboxColumn) {
    var isChecked = range.isChecked();
    var regNo = sheet.getRange(range.getRow(), regNoColumnSheet1).getValue();
    var destSheet = sheet.getParent().getSheetByName(sheet2Name);

    if (isChecked) {
      var sourceData = sheet.getRange(range.getRow(), sourceColumnsSheet1[0], 1, sourceColumnsSheet1.length).getValues()[0];
      var destData = destSheet.getRange(2, regNoColumnSheet2, destSheet.getLastRow() - 1, 1).getValues();
      var destRow = -1;

      for (var i = 0; i < destData.length; i++) {
        if (destData[i][0] === regNo) {
          destRow = i + 2;
          break;
        }
      }

      if (destRow > 1) {
        for (var i = 0; i < destColumnsSheet2.length; i++) {
          destSheet.getRange(destRow, destColumnsSheet2[i], 1, 1).setValue(sourceData[i]);
        }
        SpreadsheetApp.getActiveSpreadsheet().toast("Data transferred successfully. Registration Number matched.", "Notification");
      } else {
        SpreadsheetApp.getActiveSpreadsheet().toast("Registration Number does not exist in Sheet2.", "Notification");
      }
    } else {
      var destData = destSheet.getRange(2, regNoColumnSheet2, destSheet.getLastRow() - 1, 1).getValues();
      var destRow = -1;

      for (var i = 0; i < destData.length; i++) {
        if (destData[i][0] === regNo) {
          destRow = i + 2;
          break;
        }
      }
    }
  }
}


```

* Here's how to set up the script:

* Open your Google Sheets document.
* Click on "Extensions" in the menu, then choose "Apps Script."
* Delete any existing code in the script editor and replace it with the provided code.
* Modify the variable values in the script according to your specific needs (e.g., sheet names, column numbers).
* Save the script by clicking on the floppy disk icon or using the "File" menu.
* Close the script editor.


* Please note that this script uses the onEdit trigger, 
* which means it will run automatically whenever any cell is edited in the document. 
* Ensure that the correct checkbox column and data columns are specified in the script, matching your sheet layout.
