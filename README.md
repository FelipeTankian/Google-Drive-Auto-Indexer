# Overview of the Google Drive Auto-Indexer Script

This Google Apps Script is designed to automate the creation of a complete, organized inventory of a specific Google Drive folder and all of its contents. It extracts the data and formats it directly into a Google Spreadsheet.

Functionalities and features of the script:

* **Automated Data Extraction:** It automatically pulls metadata from your Google Drive files (File Name and Access Link) and populates a Google Sheet, eliminating the need for manual copying and pasting.
* **Deep Scanning (Recursion):** The script utilizes a programming technique called recursion. This means it doesn't just scan the surface-level files of the main folder; it dives deep into every single subfolder—and the folders inside those subfolders—ensuring no file is left behind.
* **Accurate Path Mapping:** To help you locate files easily, the script generates a "Folder Path" column. It creates a breadcrumb trail (e.g., *Main Folder > Subfolder 1 > Subfolder 2*) so you know exactly where each document is stored within your Drive hierarchy.
* **Smart Formatting and Auto-Cleaning:** Every time the script runs, it automatically clears the old data from the spreadsheet before fetching the new list. This prevents duplicate entries. It also sets up the headers, makes them bold, and freezes the top row so you can scroll through large lists comfortably.
* **Direct Access:** By generating the unique URL for every file, the spreadsheet becomes an interactive dashboard. You can click on any link to open the corresponding file directly from the sheet.
* **Background Automation Compatibility:** The script is built to be compatible with Google Apps Script's "Triggers" system. This functionality allows the code to run autonomously on a set schedule (like every night at midnight), ensuring your index is always up-to-date without any human intervention.

# How to use it:

### Phase 1: Getting Your Folder ID
1. Open Google Drive and go to the root folder you want to index.
2. Look at the URL in your browser's address bar. 
3. Copy the **Folder ID**. It is the long string of letters and numbers right after `folders/` (for example: `1aBcD2eFgH3iJkL4mNoP5qRsT6uVwXyZ` on `https://drive.google.com/drive/folders/1aBcD2eFgH3iJkL4mNoP5qRsT6uVwXyZ`).

### Phase 2: Setting up the Script in Google Sheets
1. Create a new, blank **Google Sheets** document.
2. In the top menu, click on **Extensions** > **Apps Script**. A new tab will open.
3. Delete any existing code in the editor and paste the complete script
4. On line 3, replace `PASTE_YOUR_FOLDER_ID_HERE` with the ID you copied in Phase 1. **Make sure to keep the single quotes around the ID.**
5. Click the **Save** icon (the floppy disk) at the top.

### Phase 3: Running the Script and Granting Permissions
1. Make sure `createCompleteIndex` is selected in the dropdown menu at the top.
2. Click the **Run** button (the play icon).
3. Google will ask for authorization since the script needs to access your Drive.
4. Click **Review permissions**.
5. Select your Google account.
6. You will see a "Google hasn’t verified this app" warning. Click **Advanced** at the bottom, then click **Go to Untitled project (unsafe)**.
7. Click **Allow**. 
8. Wait for the "Execution completed" message. Go back to your Google Sheet, and your index will be there!

### Phase 4: Setting up Automatic Updates (Optional)
If you want the sheet to update itself automatically (e.g., every day or week):
1. In the Apps Script editor, look at the left sidebar and click on the **clock icon** (called **Triggers**).
2. Click the blue **+ Add Trigger** button in the bottom right corner.
3. Set up the options in the pop-up window exactly like this:
   * **Choose which function to run:** `createCompleteIndex`
   * **Choose which deployment should run:** `Head`
   * **Select event source:** `Time-driven`
   * **Select type of time based trigger:** Choose your preferred frequency (e.g., `Day timer` for daily updates, or `Week timer` for weekly).
   * **Select time of day:** Choose a time window (e.g., `Midnight to 1am`).
4. Click **Save**. (You might need to grant permissions one last time, following the same steps as in Phase 3).
