

```
function myFunction() {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  const sheetNamesToProtect = ['Sheet1', 'Sheet3'];
  const password = 'YourPassword';

  let ui = SpreadsheetApp.getUi();

  let result = ui.prompt('Enter Password', ui.ButtonSet.OK);
  let button = result.getSelectedButton();
  let enteredPassword = result.getResponseText();

  if (button == ui.Button.OK && enteredPassword == password) {
    for (let i = 0; i < sheetNamesToProtect.length; i++) {
      let sheet = ss.getSheetByName(sheetNamesToProtect[i]);
      if (sheet) {
        sheet.protect().setDescription('Password Protected');
        ui.alert(`Sheet "${sheet.getName()}" protected with password successfully`);
      } else {
        ui.alert(`Sheet "${sheetNamesToProtect[i]}" not found`);
      }
    }
  } else {
    ui.alert('Invalid password');
  }
}

```
