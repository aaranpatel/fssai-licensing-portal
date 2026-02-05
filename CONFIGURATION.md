This document provides a step-by-step walkthrough on how to migrate or set up the Google Sheets backend for the FSSAI Licensing Portal.

1. Setup the New Google Sheet
Log into the target Google Account.

Create a new Google Sheet and give it a recognizable name (e.g., FSSAI_Applications_Database).

Define Headers: In the first row (Row 1), create headers that match the keys in the JavaScript formData.

Example: name, mobile, email, biz, city, pin, state, address, license_type.

2. Configure the Apps Script
Inside your new Google Sheet, navigate to Extensions > Apps Script.

Clear the Editor: Delete any default code (like function myFunction() {...}).

Paste the Backend Code: Copy and paste the .gs script provided in the repository into the editor.

Save the Project as FSSAI_Backend_Logic.

3. Deploy as a Web App (CRUCIAL STEP)
To allow the website to communicate with the sheet, you must deploy the script as a public API:

Click the Deploy button (top right) and select New Deployment.

Select Type: Click the "Gear" icon and choose Web App.

Configuration Settings:

Description: FSSAI Portal API V1

Execute As: Set this to Me (your current email address).

Who has access: Set this to Anyone.

⚠️ Warning: Do NOT choose "Anyone with a Google Account," or the form will fail for users who are not logged into a Gmail account.

Click Deploy.

4. Authorize Security Permissions
Google requires explicit permission to allow the script to write to your spreadsheet:

A popup will appear. Click Authorize Access.

Select your Account when prompted.

Bypass the Warning: You will see a "Google hasn't verified this app" screen.

Click Advanced (bottom left).

Click Go to FSSAI_Backend (unsafe).

Click Allow on the final screen.

5. Update the Frontend Code
Copy the URL: Once deployment is finished, Google will provide a Web App URL (it must end in /exec).

Open index.html: In your code editor, find the variable named scriptURL.

Replace the Link: ```javascript const scriptURL = 'PASTE_YOUR_NEW_WEB_APP_URL_HERE';

Save the file.

6. Update the Live Site
To apply the changes to the live version of your site:

For GitHub Users: Push the updated index.html to your repository.

Bash
git add index.html
git commit -m "Updated backend script endpoint"
git push origin main
For Netlify/Vercel: If your account is linked to GitHub, the site will automatically redeploy.

For Manual Hosting: If you used "Drag and Drop," simply re-upload the updated index.html to your hosting dashboard.
