# TouchPortal WebView Toast Notifications

This project allows you to display toast notifications on your TouchPortal tablet from your phone using **TouchPortal**'s WebView feature. It supports notifications from apps using **PushBullet** and **Forward SMS**, letting you see incoming messages or alerts in real time.  

---

### Features

- Real-time toast notifications from your phone to your TouchPortal tablet.
- Works with PushBullet or Forward SMS for messages.

---

### Installation

### 1. Install Node.js
Download and install [Node.js](https://nodejs.org/).

### 2. Download this repository
git clone https://github.com/xNightWulf69/TP_ToastNotifications.git

OR

Code > Download ZIP and then extract

### 3. Go to [PushBullet](https://www.pushbullet.com).
Create an account, go to My Account >  Settings > Click Create Access Token
Copy the token

### 3. Editing files
Open server.js in a text editor and edit PUSHBULLET_ACCESS_TOKEN on line 6 with the token you copied
Open Command Promt and enter `ipconfig` and press enter.
Copy your IPv4 Address
In server.js edit WS_IP on line 8 with your IPv4 Address
In server.js edit SMS_SECRET on line 7 with a password of your choosing.
Open index.html and edit WS_IP on line 31 with your IPv4 Address

### 4. Installing apps
On your mobile device install `PushBullet: SMS on PC and more` by PushBullet and install `Forward SMS` by Point Dume
Open PushBullet and login to the same Google account as you used for step 3.
Go through the setup giving any perms it needs and then go to Mirroring and enable Notification Mirroring

Now Open Forward SMS, Add rule > Basic Rule and change where to forward SMS to URL, click edit URL config and use these settings:
    Method: Post
    URL: http://127.0.0.0:3000/sms //Change 127.0.0.0 to your IPv4 Address from your PC you got earlier.
    Body:
`{
"sender": "{sender}",
"message": "{msg}",
"secret": ""  //Change this to the SMS_SECRET you set in server.js earlier.
}`

### 5. Setting up Node.js
Go to the folder where server.js is, right click and select `Open In Terminal`
In the terminal type `npm install` and press enter.
In terminal type node `server.js` and press enter //I'm sure you can get a button or something to run this as this will need to be open every time.

### 6. Touch portal
Add a webview to the page you want the notifications to be shown.
I used 3x2 for the size.
Set the webview URL to http://YOUR_IPv4_ADDRESS:3000/index.html //Make sure you change the IP to your IPv4 Address


