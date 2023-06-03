---
title: DevOps In Daily Life
date: 2022-10-05
tags: [javascript, appscript, gsuite, google]
---

## Introduction

I have been reading a lot of blogs, watching a tonne of YouTube videos, and gathering feedback from various sources about creating the perfect **Resume** and **Cover Letter**. I made atomic changes each day.

Since I was distributing these documents through a single link in a Google Drive folder, it became a monotonous, dull, boring, and tedious process to:

1. Make a few changes every day (until they are perfect).
2. Download them.
3. Delete the old ones.
4. Upload them.

I could have directly distributed the documents as *Google Docs* rather than a PDF. But,

- **Need for PDF**: A majority of employment sites demand a PDF version. The process of opening the link and exporting to PDF is still included.
- **Not Complete: Submitting an incomplete document should never be your first impression.
- **Streaming mistakes live**: There are chances of someone enjoying watching the live fixing of errors. It could occasionally be a little humiliating.

So, I had to go back to the monotonous, dull, boring, and tedious process. But this process can be automated!

## The Automaton: App Script

App Script is a low-code platform with built-in libraries inline with products from G-Suite. You can find the whole overview [here](https://developers.google.com/apps-script/overview).

Some of the amazing features that you can code are:

1. Notify when someone accesses a document.
2. Create triggers for events using third-party integrations. Example: Send a message on Discord when a Google Form is submitted.
3. Periodically export a document and email it *automatically*.
4. Populate the data, on a Google Sheets template.
5. Export your resume and cover letter to PDF.

and more. This is only limited by how well you code JS.

## In Action

In the overall process, we need to do a few things.

- Delete all the files in the folder.
- Generate a new Resume.PDF based on Resume
- Generate a new CoverLetter.PDF based on Cover Letter

**STEP 1:** Open [App Script](https://script.google.com/home) and start a new project.

**STEP 2:** Remove the boilerplate code from the project.

**STEP 3:** Paste the following code:

```js
const resumeID = DriveApp.getFileById('Your Resume Doc ID')
const coverLetterID = DriveApp.getFileById('Your Cover Letter Doc ID')
const exportFolderID = 'Your Folder ID'

function myFunction() {
// We are getting all the files present inside the folder.
const files = DriveApp.getFolderById(exportFolderID).getFiles()
// Looping over each one
while (files.hasNext()) {
files.next().setTrashed(true) // And deleting them.
}
// calling functions to automatically build and place them inside the above folder.
generateResume()
generateCoverLetter()
}

function generateResume() {
// resumeID is the ID of Google Doc file that you are automating.
var blob = resumeID.getAs('application/pdf') // getting the PDF blob (Binay Large Data), basically getting the PDF of the document as PDF.
DriveApp.getFolderById(exportFolderID) // Setting the export folder
.createFile(blob) // Creating a file from the blob
.setName('Resume') // Naming it!
}

function generateCoverLetter() {
var blob = coverLetterID.getAs('application/pdf')
DriveApp.getFolderById(exportFolderID)
.createFile(blob)
.setName('General Cover Letter')
}
```

**STEP 4:** Replace the `coverLetterID`, `resumeID` and `exportFolderID` with your specific document IDs.

The IDs can be found in the URL of the document. For example, in `https://docs.google.com/document/d/HelloThisIsTheIDOverHereAbCdEfGh123456/edit`, we need the text after `d/` and before `/edit`. Something like:

![Document ID Extraction](https://raw.githubusercontent.com/busy-in-life/Blog-Image/main/DevOpsInDailyLife/DocID.png)

The folderID will be something like `https://drive.google.com/drive/u/0/folders/HereIsTheFolderIDYouMustBeLookingFor` the last section after `folders/`. Something Like:

![Folder ID Extraction](https://raw.githubusercontent.com/busy-in-life/Blog-Image/main/DevOpsInDailyLife/FolderID.png)

- **STEP 5:** Save the script, `ctrl/cmd + s` or you will see a save icon.
- **STEP 6:** Run it! `ctrl/cmd + r` or you will see a play icon.

On the first run, you will be asked for permission. Allow them, and you will be good to go.

*Here is some pictorial flow!*

![Auth 1](/images/2_Auth1.png)
![Auth 2](/images/2_Auth2.png)
![Auth 3](/images/2_Auth3.png)

No errors in the execution log? Yes? Check the folder, and you will have your PDF versions of the documents.

Cool, now you know CI/CD🔄, automation🤖, and magicc✨!

---
