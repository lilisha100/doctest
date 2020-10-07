# Integrate with Trulioo EmbedID

**Prerequisite**:
- A Trulioo account (free)
- Any code or text editor
- [node.js](https://nodejs.org/en/)

## Step 1: Install the `trulioo-middleware` SDK
1. In the command line, run the following:
   ```
   npm install trulioo-embedid-middleware
   ```
2. The `trulioo-middleware` SDK is an `express` middleware, so you must install `express`:
   ```
   npm install express
   ```

## Step 2: Create your automated identity verification flow
1. Go to https://gateway-admin.trulioo.com/dashboard once you are logged in.
2. Click **EmbedID** in the left sidebar.
3. Click **Create New Experience**.
4. Give it a name. Let's go with "HelloWorld.”
5. Select **Identity Verification**.
6. Click **Create**.
   A "HelloWorld" identity verification flow is created.

## Step 3: Customize your identity verification flow
Your identity verification flow is created with the default setting. You can customize the prests, fields to collect, and styling of the form.

<video width="960" height="720" controls>
  <source src="customize.mp4" type="video/mp4">
</video>

## Step 4: Start your back-end service
1. Open a text editor and create a file named `backend.js`.
2. Copy and paste the following code to the `backend.js` file:
   ```
   const truliooMiddleware = require('trulioo-embedid-middleware')({ 
   apiKey: '<TRULIOO_API_KEY>' }); 
   const express = require('express'); 
   const app = express(); 
   const port = 8080;

   app.use(truliooMiddleware) 
   app.listen(port, () => console.log('Example app listening on port 8080!'));
   ```
3. Go back to your identity verification flow called “HelloWorld” and click the Edit icon.
4. In the left sidebar, click to expand the **Keys** section.
4. Locate the API Key (BE) field and copy your API Key.
5. In the `backend.js` file, replace `<TRULIOO_API_KEY>` with your API key.
6. Save your `backend.js` file to a desired location.
7. In the command line, go to the location where your `backend.js` file is saved.
8. Run the following to start your server:
   ```
   node backend.js
   ```
   If you see the 'Example app listening on port 8080!' message, you have successfully set up your server!
   
## Step 5: Set up your front-end HTML
1. Open a text editor and create a file named `index.html`.
2. Copy and paste the following code to the `index.html` file:
   ```
   <div id="trulioo-embedid"></div>

   <!-- This script renders the form for the div above --> 
   <script type="text/javascript" src="https://js.trulioo.com/latest/main.js"></script>

   <!-- Initialize your form here with your Frontend (FE) key -->
   <script> 
     // Handle the response of EmbedID after form submits
     function handleResponse(e) { 
       console.log('handleResponse', e); 
     } 

     const publicKey = 'Trial Key (FE)_OR_Live Key (FE)'; // Public Key
     // const accessTokenURL = 'http://localhost:8080/trulioo-api/embedids/tokens';
     new TruliooClient({ 
       publicKey, 
       // accessTokenURL,
       handleResponse 
     });
   </script>
   ```
3. Go back to your identity verification flow called “HelloWorld” and click the Edit icon.
4. In the left sidebar, click to expand the **Keys** section.
4. Locate the Trial Key (FE) field and copy your Trial Key.
5. In the `index.html` file, replace `Trial Key (FE)_OR_Live Key (FE)` with your Trial key.

## Step 6: We’re done! Let’s try it out
1. Open `index.html` in your browser.
2. You will see your “HelloWorld” identity verification flow appear.
3. Enter the following information in the form:

   ![](justin.png)
   
4. Click **Submmit**.
5. Go back to your dashboard, click **Transaction** and you will see a match transaction in the **Transaction History**.
