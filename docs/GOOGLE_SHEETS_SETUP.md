# Google Sheets Integration Setup Guide

## Overview
Your landing page now has a fully functional order form that pops up when users click on any pricing plan button. The form collects customer information and sends it to Google Sheets.

## What's Included

### 1. **Order Form Modal**
   - Pops up when any pricing plan button is clicked
   - Collects:
     - Full Name
     - Email Address
     - Phone Number
     - Shopify Store URL
     - Expected Monthly COD Orders
     - Additional Notes
     - Selected Plan (automatically captured)

### 2. **Features**
   - ✅ Responsive design matching your landing page
   - ✅ Form validation
   - ✅ Success/error messages
   - ✅ Automatic form reset after submission
   - ✅ Modal closes on outside click
   - ✅ Smooth animations

## Setting Up Google Sheets Integration

### Step 1: Create a Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new spreadsheet
3. Name it "Codify Orders" (or whatever you prefer)
4. Add these column headers in Row 1:
   - A1: Timestamp
   - B1: Name
   - C1: Email
   - D1: Phone
   - E1: Store URL
   - F1: Monthly Orders
   - G1: Notes
   - H1: Selected Plan

### Step 2: Create Google Apps Script

1. In your Google Sheet, go to **Extensions** → **Apps Script**
2. Delete any code in the editor
3. Paste this code:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var data = JSON.parse(e.postData.contents);
    
    // Add row to sheet
    sheet.appendRow([
      data.timestamp,
      data.name,
      data.email,
      data.phone,
      data.storeUrl,
      data.monthlyOrders,
      data.notes,
      data.selectedPlan
    ]);
    
    return ContentService.createTextOutput(JSON.stringify({
      'status': 'success'
    })).setMimeType(ContentService.MimeType.JSON);
    
  } catch(error) {
    return ContentService.createTextOutput(JSON.stringify({
      'status': 'error',
      'message': error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}
```

4. Click **Save** (💾 icon)
5. Name your project (e.g., "Codify Form Handler")

### Step 3: Deploy the Web App

1. Click **Deploy** → **New deployment**
2. Click the gear icon ⚙️ next to "Select type"
3. Choose **Web app**
4. Fill in the settings:
   - **Description**: "Codify Order Form"
   - **Execute as**: Me
   - **Who has access**: Anyone
5. Click **Deploy**
6. **Authorize** the app (click "Authorize access")
7. Sign in with your Google account
8. Click **Advanced** → **Go to [Your Project Name] (unsafe)**
9. Click **Allow**
10. **Copy the Web App URL** - it looks like:
    ```
    https://script.google.com/macros/s/XXXXXXXXXXXXX/exec
    ```

### Step 4: Update Your HTML File

1. Open `codify-landing.html`
2. Find this line (around line 3280):
   ```javascript
   const GOOGLE_SHEETS_URL = 'YOUR_GOOGLE_SHEETS_WEB_APP_URL_HERE';
   ```
3. Replace `'YOUR_GOOGLE_SHEETS_WEB_APP_URL_HERE'` with your copied Web App URL:
   ```javascript
   const GOOGLE_SHEETS_URL = 'https://script.google.com/macros/s/XXXXXXXXXXXXX/exec';
   ```
4. Save the file

## Testing

1. Open your `codify-landing.html` in a browser
2. Scroll to the pricing section
3. Click any "Get Started", "Start Trial", or "Contact Sales" button
4. Fill out the form
5. Click "Submit Order"
6. Check your Google Sheet - the data should appear!

## How It Works

1. **User clicks a pricing button** → Modal opens with the selected plan
2. **User fills out form** → Data is validated
3. **User submits** → Data is sent to Google Sheets via the Web App
4. **Success message shows** → Form resets and modal closes after 3 seconds

## Customization

### Change Form Fields

Edit the form in the HTML around line 3195-3270 to add/remove fields.

### Change Form Styling

All form elements use Tailwind CSS classes. Modify them to match your brand.

### Email Notifications

To get email notifications when someone submits the form, add this to your Apps Script:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var data = JSON.parse(e.postData.contents);
    
    // Add row to sheet
    sheet.appendRow([
      data.timestamp,
      data.name,
      data.email,
      data.phone,
      data.storeUrl,
      data.monthlyOrders,
      data.notes,
      data.selectedPlan
    ]);
    
    // Send email notification
    MailApp.sendEmail({
      to: "your-email@example.com",  // Replace with your email
      subject: "New Codify Order: " + data.selectedPlan + " Plan",
      body: `
        New order received!
        
        Plan: ${data.selectedPlan}
        Name: ${data.name}
        Email: ${data.email}
        Phone: ${data.phone}
        Store: ${data.storeUrl}
        Monthly Orders: ${data.monthlyOrders}
        Notes: ${data.notes}
      `
    });
    
    return ContentService.createTextOutput(JSON.stringify({
      'status': 'success'
    })).setMimeType(ContentService.MimeType.JSON);
    
  } catch(error) {
    return ContentService.createTextOutput(JSON.stringify({
      'status': 'error',
      'message': error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}
```

## Troubleshooting

### Form doesn't submit
- Make sure you've updated the `GOOGLE_SHEETS_URL` in the HTML
- Check browser console for errors (F12 → Console tab)

### Data not appearing in Sheet
- Verify your Apps Script is deployed as a Web App
- Make sure "Who has access" is set to "Anyone"
- Check the Apps Script execution logs: Apps Script → Executions

### Authorization issues
- You may need to re-authorize if you change the script
- Go to Deploy → Manage deployments → Edit → Deploy

## Support

If you need help, check:
- Google Apps Script [documentation](https://developers.google.com/apps-script)
- Your browser's developer console for error messages

---

**Note**: The form uses `mode: 'no-cors'` which means it won't show detailed errors. This is normal for Google Sheets Web Apps. The success message will show after submission regardless of whether it worked. Check your Google Sheet to verify data is being saved.
