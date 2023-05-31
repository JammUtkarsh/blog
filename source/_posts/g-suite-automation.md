---
title: DevOps In Daily Life
date: 2022-10-05
tags: [javascript]
---

It is the time of year when I am applying for internships. I'm reading blogs, watching YouTube videos, and feedback from various sources. To get the perfect output of "How to create the ideal resume and cover letter?" This is not a blog where I teach you how to write the perfect the professional documents(**pro-docs** like resumes and cover-letters). Instead, I will help you save some time.

I usually spend an hour or so in researching and developing pro-docs daily, rather than spending a whole day on it. Since, I improvise on almost daily basis, the pro-docs needs to be exported to PDF. My preferred tool for creating pro-docs is Google Docs (**G-Docs**), which is a part of G-Suite (*Too many GGGGs*). The PDF is then uploaded to a publicly available folder (like Google Drive) so that I may distribute them on GitHub, LinkedIn, and other sites.
It becomes monotonous, dull, burdensome, boring, tedious to:

1. Make a few changes every day(until the pro-docs are prefect).
2. Download them.
3. Delete the old ones.
4. Upload them.

One strategy would be to distribute the pro-docs directly as a link to the document, rather than a PDF. But,

1. **Need for PDF**: The majority of employment sites demand that you submit your professional documents as a PDF. The process of opening the link and exporting to PDF is still included, if you are the one doing it.
2. **!Complete**: If I haven't  revised the errors, this document will be available online in a partially complete state. Could be deadly
3. **Streaming mistakes live**: If you are revising them and someone is looking at your resume simultaneously. They may watch your mistakes and advancements being made in real time. It could occasionally be a little humiliating.

The monotonous, dull, burdensome, boring, tedious tasks that I mentioned can be automated!

## App Script: The Automaton

It is Google's flavor of JavaScript and a low-code platform to programmatically automate Google Suite line of products. You can find the whole overview [here](https://developers.google.com/apps-script/overview).
A few features, which I discovered:

1. Notifies us is someone accesses our document.
2. Can send messages using 3rd party integration to Discord or Slack channels when an event is triggered. (say a Google Form is submitted.)
3. Export PDF and send mail of some reports.
4. Upload data and use the template of a Google Sheet to automatically populate it.
5. Export Resume and Cover Letter to PDF.

The list is only limited by your creativity. In the end, it comes down to programming!

*PS:Additionally, you gained a basic understanding of continuous integration and delivery (CI/CD). Continuously integrating changes to the pro-docs; continuously delivering pro-docs to various platforms.*

### Technical Overview

In the snippet below, are going to:

- Delete all the files in the folder.
- Generate a new Resume.PDF
- Generate a new CoverLetter.PDF

### Steps to reproduce

- **STEP 1:** Open [App Script](https://script.google.com/home) and start a new project.
- **STEP 2:** Remove the boilerplate code from the project
- **STEP 3:** Paste the following code

```js
const resumeID = DriveApp.getFileById('Your Resume Doc ID')
const coverLetterID = DriveApp.getFileById('Your Cover Letter Doc ID')
const exportFolderID = 'Your Folder ID'

function myFunction() {
// We are getting all the files present inside folder.
  const files = DriveApp.getFolderById(exportFolderID).getFiles()
// Looping over each one
  while (files.hasNext()) {
    files.next().setTrashed(true) // And deleting them.
  }
  // Calling functions to automatically build and place them inside the above folder.
  generateResume()
  generateCoverLetter()
}

function generateResume() {
// resumeID is Google Doc file whcih you are automating.
  var blob = resumeID.getAs('application/pdf') // getting the PDF blob(Binay Large Data), basically getting PDF of document as PDF.
  DriveApp.getFolderById(exportFolderID) // Setting the export folder
    .createFile(blob) // Creating a file from the BLOB
    .setName('Resume') // Naming it!
}

function generateCoverLetter() {
  var blob = coverLetterID.getAs('application/pdf')
  DriveApp.getFolderById(exportFolderID)
    .createFile(blob)
    .setName('General Cover Letter')
}
```

- **STEP 4:** Replace the `coverLetterID`, `resumeID` and `exportFolderID` with your specific document IDs.

These IDs are present in the URL when you open the document in a tab.
For example, `https://docs.google.com/document/d/HelloThisIsTheIDOverHereAbCdEfGh123456/edit`, we need the portion after `d/` and before `/edit`. Something like:

![Document ID Extraction](https://raw.githubusercontent.com/busy-in-life/Blog-Image/main/DevOpsInDailyLife/DocID.png)

The folderID will be something like `https://drive.google.com/drive/u/0/folders/HereIsTheFolderIDYouMustBeLookingFor` the last section after `folders/`.  Something Like:

![Folder ID Extraction](https://raw.githubusercontent.com/busy-in-life/Blog-Image/main/DevOpsInDailyLife/FolderID.png)

- **STEP 5:** Save the script, `ctrl/cmd + s` or you will see a save icon
- **STEP 6:** Run it! `ctrl/cmd + r` or you will see a play icon

On the first run, you will be asked for permission. Allow them and you will be good to go.

*Here is some pictorial flow!*

![1](/images/DevOpsInDailyLife2/Auth1.png)
![2](/images/DevOpsInDailyLife2/Auth2.png)
![3](/images/DevOpsInDailyLife2/Auth3.png)

No errors in the execution log? Yes? Check the folder, and you will have your PDF versions of the pro-docs.
