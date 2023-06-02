### script for protect google sheets
* Just Copy and Paste the Script on Google Sheet Editor
* Setup the Trigger

```
function myFunction() {
  ss = SpreadsheetApp.getActiveSpreadsheet();
  let pwd ='';
  let ui = SpreadsheetApp.getUi();
  let bt = ui.Button.CANCEL;
  let result = ui.prompt('Enter Password', ui.ButtonSet.OK);
  let button = result.getSelectedButton();
  topic = result.getResponseText();
  if(button == ui.Button.OK && topic == 'UnboxGenie'){
ui.alert('Password entered successfully');
  }
    else{
      while(pwd != 'UnboxGenie' || bt != ui.Button.OK){
let pmt = ui.prompt('Providing password is mandatory', ui.ButtonSet.OK);
pwd = pmt.getResponseText();
bt = pmt.getSelectedButton();
      }
      ui.alert('Password entered successfully');
    }
  }
  
  ```
