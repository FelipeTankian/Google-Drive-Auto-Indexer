# How to use it:



Here is the complete, step-by-step guide in English on how to set up, run, and automate the script. 



\### Phase 1: Getting Your Folder ID

1\. Open Google Drive and go to the root folder you want to index.

2\. Look at the URL in your browser's address bar. 

3\. Copy the \*\*Folder ID\*\*. It is the long string of letters and numbers right after `folders/` (for example: **1aBcD2eFgH3iJkL4mNoP5qRsT6uVwXyZ** on `https://drive.google.com/drive/folders/1aBcD2eFgH3iJkL4mNoP5qRsT6uVwXyZ`).



\### Phase 2: Setting up the Script in Google Sheets

1\. Create a new, blank \*\*Google Sheets\*\* document.

2\. In the top menu, click on \*\*Extensions\*\* > \*\*Apps Script\*\*. A new tab will open.

3\. Delete any existing code in the editor and paste the complete script

4\. On line 3, replace `PASTE\_YOUR\_FOLDER\_ID\_HERE` with the ID you copied in Phase 1. \*\*Make sure to keep the single quotes around the ID.\*\*

5\. Click the \*\*Save\*\* icon (the floppy disk) at the top.



\### Phase 3: Running the Script and Granting Permissions

1\. Make sure `createCompleteIndex` is selected in the dropdown menu at the top.

2\. Click the \*\*Run\*\* button (the play icon).

3\. Google will ask for authorization since the script needs to access your Drive.

4\. Click \*\*Review permissions\*\*.

5\. Select your Google account.

6\. You will see a "Google hasn’t verified this app" warning. Click \*\*Advanced\*\* at the bottom, then click \*\*Go to Untitled project (unsafe)\*\*.

7\. Click \*\*Allow\*\*. 

8\. Wait for the "Execution completed" message. Go back to your Google Sheet, and your index will be there!



\### Phase 4: Setting up Automatic Updates (Optional)

If you want the sheet to update itself automatically (e.g., every day or week):

1\. In the Apps Script editor, look at the left sidebar and click on the \*\*clock icon\*\* (called \*\*Triggers\*\*).

2\. Click the blue \*\*+ Add Trigger\*\* button in the bottom right corner.

3\. Set up the options in the pop-up window exactly like this:

&#x20;  \* \*\*Choose which function to run:\*\* `createCompleteIndex`

&#x20;  \* \*\*Choose which deployment should run:\*\* `Head`

&#x20;  \* \*\*Select event source:\*\* `Time-driven`

&#x20;  \* \*\*Select type of time based trigger:\*\* Choose your preferred frequency (e.g., `Day timer` for daily updates, or `Week timer` for weekly).

&#x20;  \* \*\*Select time of day:\*\* Choose a time window (e.g., `Midnight to 1am`).

4\. Click \*\*Save\*\*. (You might need to grant permissions one last time, following the same steps as in Phase 3).

