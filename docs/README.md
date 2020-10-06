# Integrate Trulioo EmbedID into Your KYC
Prerequisite:
- A Trulioo account (free)
- Any code or text editor
- [node.js](https://nodejs.org/en/)

## Step 1: Install the `trulioo-middleware` SDK
1. In the command line, run the following:
   ```
   npm install trulioo-embedid-middleware
   ```
2. The `trulioo-middleware` SDK is an `express` middleware. The next step is to install the `express`:
   ```
   npm install express
   ```
## Step 2: Create your automated identity verification flow
1. Go to https://gateway-admin.trulioo.com/dashboard once you are logged in.
2. Click **EmbedID** in the left navbar.
3. Click **Create New Experience**.
4. Give it a name. Let's go with "HelloWorld.”
5. Select **Identity Verification**.
6. Click **Create**.
   A "HelloWorld" identity verification flow is created.

## Step 3: Customize your identity verification flow
Your identity verification flow is created with the default setting. You can customize the prests, fields to collect, and styling of the form.

<iframe class="embeddedObject shadow resizable" name="embedded_content" scrolling="no" frameborder="0" type="text/html" 
        style="overflow:hidden;" src="https://www.screencast.com/users/lilisha100/folders/Capture/media/30a4721b-f2c6-4ea1-8f51-c3f9a799bac3/embed" height="1080" width="1474" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

## Step 3: Start your back-end service
1. Open a text editor and create a file named `backend.js`.
2. Copy and paste the following code to the `backend.js` file:
   ```
   const truliooMiddleware = require('trulioo-embedid-middleware')({ 
   apiKey: <TRULIOO_API_KEY> }); 
   const express = require('express'); 
   const app = express(); 
   const port = 8080;

   app.use(truliooMiddleware) 
   app.listen(port, () => console.log('Example app listening on port ${port}!'));
   ```
 3. Go back to your identity verification flow called “HelloWorld” in the left sidebar and click to expand the **Keys** section.
 4. Locate the API Key (BE) field and click the  icon to copy your API Key.
 5. Replace the `<TRULIOO_API_KEY>` with your API key in the `backend.js` file.
 6. Save your `backend.js` file to a desired location in your computer.
 7. In the command line, go to the location where your `backend.js` file is saved.
 8. Run the following to start your server:
    ```
    node backend.js
    ```
