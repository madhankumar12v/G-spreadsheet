### Remove duplicate In column "G" using Custom Menu Button

```

function onOpen() {
  SpreadsheetApp.getUi().createMenu('Custom Menu')
    .addItem('Check for Duplicates', 'checkForDuplicates')
    .addToUi();
}

function checkForDuplicates() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('stat-tr'); // Replace with your actual sheet name
  var columnC = sheet.getRange('G:G');
  var values = columnC.getValues();
  var duplicates = [];
  var uniqueValues = [];

  for (var i = 0; i < values.length; i++) {
    if (values[i][0] !== '') {
      var currentValue = values[i][0];

      // Check for duplicates
      if (uniqueValues.indexOf(currentValue) === -1) {
        uniqueValues.push(currentValue);
      } else {
        duplicates.push(currentValue);
        values[i][0] = 'Duplicate';
      }
    }
  }

  columnC.setValues(values);

  if (duplicates.length > 0) {
    SpreadsheetApp.getActiveSpreadsheet().toast('Duplicates have been replaced with "Duplicate" in column C.', 'Duplicate Replacement', 5);
  }

  Logger.log('Unique values: ' + uniqueValues);
}


```
