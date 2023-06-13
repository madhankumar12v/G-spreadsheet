### Backup Apps script

* 1.Move data based on Checkbox

```
function onEdit2(e) {
  var sourceSheet = e.source.getActiveSheet();
  var targetSheet = e.source.getSheetByName("Tracker");
  var range = e.range;

  // Check if the edited cell is in the desired column (e.g., column A for the checkbox)
  if (range.getColumn() == 94) {
    // Check if the edited cell is checked
    if (range.isChecked()) {
      var row = range.getRow();
      var lastColumn = sourceSheet.getLastColumn();
      var sourceData = sourceSheet.getRange(row, 1, 1, lastColumn).getValues()[0];

      var sourceSelectedColumns = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95]; // Specify the source selected column numbers
      var targetSelectedColumns = [2,3,4,5,6,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98]; // Specify the target selected column numbers

      // Find the next available row in Sheet2 for columns 2 to 95
      var targetRow = 1;
      var targetRange = targetSheet.getRange(targetRow, 2, targetSheet.getLastRow(), 94);
      var targetValues = targetRange.getValues();
      while (targetRow <= targetSheet.getLastRow() && targetValues[targetRow - 1].join("") != "") {
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

      // Display a message
      Browser.msgBox("Data moved successfully!");
    }
  }
}

```
* 2.Copy data based on Checkbox

```
function onEdit(e) {
  var sourceSheet = e.source.getActiveSheet();
  var targetSheet = e.source.getSheetByName("Tracker");
  var range = e.range;

  // Check if the edited cell is in the desired column (e.g., column A for the checkbox)
  if (range.getColumn() == 102) {
    // Check if the edited cell is checked
    if (range.isChecked()) {
      var row = range.getRow();
      var lastColumn = sourceSheet.getLastColumn();
      var sourceData = sourceSheet.getRange(row, 1, 1, lastColumn).getValues()[0];

      var sourceSelectedColumns = [14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103]; // Specify the source selected column numbers
      var targetSelectedColumns = [9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98]; // Specify the target selected column numbers

      // Find the next available row in Sheet2 for columns 2 to 95
      var targetRow = 1;
      var targetRange = targetSheet.getRange(targetRow, 2, targetSheet.getLastRow(), 94);
      var targetValues = targetRange.getValues();
      while (targetRow <= targetSheet.getLastRow() && targetValues[targetRow - 1].join("") != "") {
        targetRow++;
      }

      // Move the data to the next available row in Sheet2
      for (var i = 0; i < sourceSelectedColumns.length; i++) {
        var sourceColumn = sourceSelectedColumns[i];
        var targetColumn = targetSelectedColumns[i];
        targetSheet.getRange(targetRow, targetColumn).setValue(sourceData[sourceColumn - 1]);
      }
       var copiedRow = sourceSheet.getRange(row, 1).getRow();
      SpreadsheetApp.getActiveSpreadsheet().toast("Row " + copiedRow + " Successfully Data copied to Tracker", "Success", 3);
    }
  }
} 

```
* 3.Push data based on Checkbox

```
function onEdit1(e) {
  var sheet1Name = "Reference";
  var sheet2Name = "V-Bookings";
  var checkboxColumn = 12; // Column L
  var regNoColumnSheet1 = 28; // Column AB in Reference
  var regNoColumnSheet2 = 1; // Column A in V-Bookings
  var sourceColumnsSheet1 = [29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71]; // Columns M, N, O, P, Q, R, S, T, U, V in Sheet1
  var destColumnsSheet2 = [23,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92]; // Columns AI, AJ, AO, AP, AZ, BG, BC, BJ, S, T in Sheet2

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
        SpreadsheetApp.getActiveSpreadsheet().toast("Data transferred successfully. Internal ID matched.", "Notification");
      } else {
        SpreadsheetApp.getActiveSpreadsheet().toast("Internal ID does not exist in V-Bookings.", "Notification");
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


