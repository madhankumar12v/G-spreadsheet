### Script for Specific sheet Protect with Password

* Just Copy and Paste the Script

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

* In this modified code, a password variable password is defined with the desired password for protecting the sheets. After prompting the user to enter the password, the code checks if the entered password matches the expected password. If the passwords * * match, it iterates over the sheet names in the sheetNamesToProtect array, retrieves each sheet, and protects it using protect(). The setDescription() method is used to provide a description for the protection. Finally, alerts are shown indicating **  whether each sheet has been protected with a password or if the sheet was not found.

* Remember to replace 'YourPassword' with the actual password you want to use for protecting the sheets.
