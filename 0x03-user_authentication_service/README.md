User Authentication 2.0
This is a sample implementation of the User Authentication service for Bungie.net. See the Official Help Article for more information.

Pre-Setup: Choose OAuth Client Type
This setting has to match what was set in your application settings. This is set when you create your app, but this demo allows you to switch between them to see the differences in the implementation.

OAuth Client Type

Public
This client type is useful for client side implementations where your authentication calls are exposed.

Page Redirect
Open In A New Tab
Step 1: Ask the user to Authorize your app
This is the Authorization URL found under each API Key after you have setup your Redirect URL.

Example Authorization URL
https://www.bungie.net/en/OAuth/Authorize?client_id={client-id}&response_type=code
Step 2: Send Authorization Code to the GetOAuthAccessToken endpoint.
Once the user has approved your App, Bungie.net will redirect them back to the Redirect URL you specified in your Application Settings with ?code={your-authentication-code} appended to end of the url. From this point on, you no longer need user interaction so this should all be done automatically.

Step 3: Test Authenticated APIs
Make sure to store the Access Token and Refresh Token somewhere safe. In the case of this Angular app, they have been stored in Local Storage.

Step 4: Renew Access Tokens (Confidential Only)
Access Tokens only last for one hour so your App needs to make a request to GetOAuthAccessToken to renew it using your Refresh Token. Refresh Tokens last up to 90 days and get renewed for another 90 days every time you call this endpoint up to a maximum of 1 year at which point all your tokens will be voided and your user is sent back to Step 1.