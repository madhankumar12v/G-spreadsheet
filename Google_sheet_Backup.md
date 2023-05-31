### Here's an example of an Apps Script code that can be used to create backups of a Google Sheets file:

```
function createSheetBackup() {
  var spreadsheetId = 'YOUR_SPREADSHEET_ID'; // Replace with your Google Sheets file ID
  var backupFolderId = 'YOUR_BACKUP_FOLDER_ID'; // Replace with the ID of the folder where you want to store the backups
  
  var spreadsheet = SpreadsheetApp.openById(spreadsheetId);
  var sheetName = spreadsheet.getName();
  
  var timestamp = Utilities.formatDate(new Date(), SpreadsheetApp.getActive().getSpreadsheetTimeZone(), 'yyyyMMdd_HHmmss');
  var backupName = sheetName + '_' + timestamp;
  
  var backupSheet = spreadsheet.copy(backupName);
  var backupFile = DriveApp.getFileById(backupSheet.getId());
  
  var backupFolder = DriveApp.getFolderById(backupFolderId);
  backupFolder.createFile(backupFile);
  
  // Optional: Delete older backups to avoid cluttering the folder
  var backupFiles = backupFolder.getFilesByName(sheetName);
  while (backupFiles.hasNext()) {
    var file = backupFiles.next();
    if (file.getName() !== backupName) {
      file.setTrashed(true);
    }
  }
  
  Logger.log('Backup created: ' + backupName);
}

```

*To use this script:

*Open your Google Sheets file.
* Go to "Extensions" in the menu, then click on "Apps Script".
* Replace the values 'YOUR_SPREADSHEET_ID' and 'YOUR_BACKUP_FOLDER_ID' with the appropriate IDs. You can find the spreadsheet ID in the URL of your Google Sheets file, and the folder ID can be obtained from the folder's URL or by right-clicking on the folder and selecting "Get link".
* Save the script and give it a name.
* Run the createSheetBackup function by clicking on the play button or selecting it from the toolbar.
* The script will create a backup of the Google Sheets file and store it in the specified backup folder. The backup file will have the format SHEET_NAME_TIMESTAMP.
* You can schedule this script to run automatically by using Google Apps Script's time-driven triggers. To set up a trigger, go to the "Triggers" section in the Apps Script editor and configure it according to your desired schedule.
