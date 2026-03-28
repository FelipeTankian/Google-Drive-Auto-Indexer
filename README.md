# Google Drive Auto-Indexer (Optimized)

An automated, high-performance Google Apps Script that generates a complete, organized inventory of a specific Google Drive folder and all its contents, outputting the data directly into a Google Spreadsheet. 

This version is highly optimized using batch operations (arrays) to prevent the common "Exceeded maximum execution time" error in Google Apps Script, making it suitable for large directories.

## 📖 Overview

This script is designed to save time by eliminating manual data entry when organizing large Google Drive directories. It deeply scans a root folder, maps out the exact path of every file, and provides direct access links in a clean, auto-updating spreadsheet. 

## ✨ Features

* **High-Performance Batch Writing:** Instead of writing row by row (which is slow and triggers Google's 6-minute execution limit), the script stores data in memory and outputs thousands of rows instantly at the very end.
* **Automated Data Extraction:** Automatically pulls metadata (File Name and Access Link) from Google Drive files and populates a Google Sheet.
* **Deep Scanning (Recursion):** Dives deep into every single subfolder—and the folders inside those subfolders—ensuring no file is left behind.
* **Accurate Path Mapping:** Generates a "Folder Path" column, creating a breadcrumb trail (e.g., *Main Folder > Subfolder 1 > Subfolder 2*) so you know exactly where each document is stored.
* **Smart Formatting and Auto-Cleaning:** Clears old data before fetching the new list to prevent duplicates. It automatically makes headers bold and freezes the top row for comfortable scrolling.
* **Direct Access:** Generates unique URLs for every file, turning your spreadsheet into an interactive dashboard.
* **Background Automation:** Compatible with Google Apps Script's "Triggers" system, allowing the code to run autonomously on a set schedule (e.g., daily or weekly).

## 🚀 How to Use

### Phase 1: Getting Your Folder ID
1. Open Google Drive and go to the root folder you want to index.
2. Look at the URL in your browser's address bar. 
3. Copy the **Folder ID**. It is the long string of letters and numbers right after `folders/` (for example: `1aBcD2eFgH3iJkL4mNoP5qRsT6uVwXyZ`).

### Phase 2: Setting up the Script in Google Sheets
1. Create a new, blank **Google Sheets** document.
2. In the top menu, click on **Extensions** > **Apps Script**. 
3. Delete any existing code in the editor and paste the optimized script below:

```javascript
function createCompleteIndex() {
  // Replace the text below with your root folder ID
  var rootFolderId = 'PASTE_YOUR_FOLDER_ID_HERE'; 
  
  var rootFolder = DriveApp.getFolderById(rootFolderId);
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  
  // Clears the current sheet and creates the headers
  sheet.clear();
  sheet.appendRow(["File Name", "Folder Path", "Access Link"]);
  sheet.getRange("A1:C1").setFontWeight("bold");
  sheet.setFrozenRows(1);
  
  var initialPath = rootFolder.getName();
  
  // Creates an empty array in memory to store data temporarily (Optimized approach)
  var allData = []; 
  
  // Scans folders and fills the array with data
  listFilesInFolder(rootFolder, initialPath, allData);
  
  // Once scanning is complete, writes all data to the sheet at once
  if (allData.length > 0) {
    sheet.getRange(2, 1, allData.length, 3).setValues(allData);
  }
}

// This is the "helper" function that does the repetitive work (recursion)
function listFilesInFolder(folder, path, allData) {
  var files = folder.getFiles();
  while (files.hasNext()) {
    var file = files.next();
    // Instead of writing to the sheet immediately, it stores in memory (allData)
    allData.push([file.getName(), path, file.getUrl()]); 
  }
  
  var subfolders = folder.getFolders();
  while (subfolders.hasNext()) {
    var subfolder = subfolders.next();
    var newPath = path + " > " + subfolder.getName();
    listFilesInFolder(subfolder, newPath, allData);
  }
}
```

4. On line 3 of the code, replace `PASTE_YOUR_FOLDER_ID_HERE` with your actual folder ID (keep the single quotes).
5. Click the **Save** icon (the floppy disk).

### Phase 3: Running the Script and Granting Permissions
1. Make sure `createCompleteIndex` is selected in the dropdown menu at the top of the editor.
2. Click the **Run** button.
3. Google will ask for authorization to access your Drive. Click **Review permissions**.
4. Select your Google account.
5. On the "Google hasn’t verified this app" warning, click **Advanced** at the bottom, then click **Go to Untitled project (unsafe)**.
6. Click **Allow**. 
7. Wait for the "Execution completed" message. Your index is ready in the Google Sheet!

## ⏱️ Setting up Automatic Updates (Optional)
If you want the sheet to update itself automatically in the background:
1. In the Apps Script editor, click on the **clock icon** (Triggers) on the left sidebar.
2. Click the blue **+ Add Trigger** button in the bottom right corner.
3. Set the options as follows:
   * **Choose which function to run:** `createCompleteIndex`
   * **Choose which deployment should run:** `Head`
   * **Select event source:** `Time-driven`
   * **Select type of time based trigger:** Choose your frequency (e.g., `Day timer` or `Week timer`).
   * **Select time of day:** Choose a time window (e.g., `Midnight to 1am`).
4. Click **Save** and grant permissions if prompted.
