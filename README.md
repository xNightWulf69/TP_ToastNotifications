# TouchPortal WebView Toast Notifications

This project allows you to display toast notifications on your TouchPortal tablet from your phone using TouchPortal's WebView feature. It supports notifications from apps like PushBullet and Forward SMS, letting you see incoming messages or alerts in real time.

---

### Features

- Real-time toast notifications from your phone to your TouchPortal tablet.
- Works with PushBullet or Forward SMS for messages.

---

### Installation

### 1. Install Node.js
Download and install [Node.js](https://nodejs.org/).

### 2. Download this repository
You can either:
   git clone https://github.com/xNightWulf69/TP_ToastNotifications.git

OR

   Click Code > Download ZIP on GitHub
   Extract the ZIP to a folder of your choice

### 3. Set Up PushBullet
Go to [PushBullet](https://www.pushbullet.com) and create an account.
Navigate to My Account > Settings > Create Access Token.
Copy the access token.

### 3. Configure the Project
Open server.js in a text editor>
- Edit `PUSHBULLET_ACCESS_TOKEN` (line 6) with the PushBullet token you copied
- Set `SMS_SECRET` (line 7) to a password of your choice.
- Set `WS_IP` (line 8) to your computer's IPv4 address.

Find your IPv4 address:
Windows: Open Command Prompt → ipconfig → Copy IPv4 Address
In `server.js` Set `WS_IP` (line 8) to your computer's IPv4 address.
Open `index.html` and edit `WS_IP` (line 31) with your IPv4 Address

### 4. Install Phone Apps
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

### 5. Install Node Dependencies
Go to the folder where server.js is, right click and select `Open In Terminal`
In the terminal type `npm install` and press enter.
In terminal type `node server.js` and press enter //I'm sure you can get a button or something to run this as this will need to be open every time.

### 6. Set Up TouchPortal
Add a webview to the page you want the notifications to be shown.
I used 3x2 for the size.
Set the webview URL to http://YOUR_IPv4_ADDRESS:3000/index.html //Make sure you change the IP to your IPv4 Address

### Usage

Notifications from PushBullet or Forward SMS will now appear as toast notifications on your TouchPortal tablet.

Customize sounds by replacing notification.mp3 in the sounds/ folder. //Must still be called notification.mp3

### Troubleshooting
- Ensure your phone and PC are on the same local network.


