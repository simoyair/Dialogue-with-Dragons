# Google Sheets Integration Instructions for Dialogue with Dragons Contact Form

## Overview
This document provides step-by-step instructions to connect your contact form to Google Sheets using Google Apps Script. This will allow form submissions to be automatically saved to a spreadsheet.

## Step 1: Create Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Click "Blank" to create a new spreadsheet
3. Name it "DwD Landing Page Submissions"
4. In row 1, add these column headers:
   - A1: `Timestamp`
   - B1: `Name`
   - C1: `Phone`
   - D1: `Contact Method`
   - E1: `Contact ID`
   - F1: `About Yourself`
   - G1: `Program Understanding`
   - H1: `Money-back Acknowledgment`

## Step 2: Add Google Apps Script

1. In your Google Sheet, click **Extensions** → **Apps Script**
2. Delete all the default code in the editor
3. Copy and paste this code:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var timestamp = new Date();
    
    // Get form data
    var data = [
      timestamp,
      e.parameter.name || '',
      e.parameter.phone || '',
      e.parameter.contactMethod || '',
      e.parameter.contactId || '',
      e.parameter.aboutYourself || '',
      e.parameter.programUnderstanding ? 'Yes' : 'No',
      e.parameter.moneybackAcknowledgment ? 'Yes' : 'No'
    ];
    
    // Add the data to the sheet
    sheet.appendRow(data);
    
    // Return success response
    return ContentService.createTextOutput(JSON.stringify({result: "success"}))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    // Log error and return error response
    console.error('Error:', error);
    return ContentService.createTextOutput(JSON.stringify({result: "error", message: error.toString()}))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

4. Click **Save** (Ctrl+S or Cmd+S)
5. Name the project "Form Submission Handler"

## Step 3: Deploy Web App

1. Click **Deploy** → **New deployment**
2. Click the gear icon ⚙️ next to "Type" and select **Web app**
3. Set the following options:
   - **Execute as**: Me (your-email@gmail.com)
   - **Who has access**: Anyone
4. Click **Deploy**
5. **Copy the Web App URL** - you'll need this for the next step
6. Click **Done**

## Step 4: Update Your Form

1. Open your `index.html` file
2. Find the form element: `<form id="contactForm" action="#" method="POST">`
3. Replace `action="#"` with your Web App URL:
   ```html
   <form id="contactForm" action="YOUR_WEB_APP_URL_HERE" method="POST">
   ```
4. Save the file

## Step 5: Test the Integration

1. Open your website in a browser
2. Fill out and submit the contact form
3. Check your Google Sheet - you should see a new row with the form data
4. Verify the thank-you page opens in a new tab

## Troubleshooting

### If submissions don't appear in the sheet:
1. Check that the Web App URL is correct in your form
2. Make sure the Apps Script deployment is set to "Anyone" access
3. Check the browser's developer console (F12) for any error messages
4. Verify the Apps Script code is saved and deployed

### If you get permission errors:
1. Make sure you're signed into the correct Google account
2. Ensure the Google Sheet and Apps Script are in the same account
3. Try redeploying the web app

### If the form doesn't submit:
1. Check that all required fields are filled
2. Verify the form validation is working (try with missing fields)
3. Check that the character counter is working (50-300 characters)

## Security Notes

- The web app is set to "Anyone" access, which means it can receive submissions from your website
- Form data is stored in your Google Sheet, which only you can access
- No sensitive information is exposed through the web app URL

## Customization

You can modify the Apps Script code to:
- Add email notifications when forms are submitted
- Format the data differently
- Add validation or filtering
- Send auto-replies to form submitters

## Support

If you encounter issues:
1. Check the Google Apps Script documentation
2. Verify your Google account permissions
3. Test with a simple form first before using the full contact form

---

**Important**: Keep your Web App URL private and don't share it publicly, as it allows form submissions to your sheet.
