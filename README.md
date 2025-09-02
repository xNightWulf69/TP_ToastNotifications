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
Open config.json in a text editor>
- Edit `PUSHBULLET_ACCESS_TOKEN` (line 2) with the PushBullet token you copied
- Set `SMS_SECRET` (line 3) to a password of your choice.

### 4. Install Phone Apps
On your mobile device install `PushBullet: SMS on PC and more` by PushBullet and install `Forward SMS` by Point Dume
Open PushBullet and login to the same Google account as you used for step 3.
Go through the setup giving any perms it needs and then go to Mirroring and enable Notification Mirroring

On your PC open Command promt and do the follow command: `for /f "tokens=2 delims=:" %a in ('ipconfig ^| find "IPv4"') do @echo %a`

Now Open Forward SMS, Add rule > Basic Rule and change where to forward SMS to URL, click edit URL config and use these settings:
    Method: `Post`
    URL: `http://<IPv4Address>:3000/sms` //Change <IPv4Address> to the address you just got from Command Prompt
    Body:
`{
"sender": "{sender}",
"message": "{msg}",
"secret": ""  //Change this to the SMS_SECRET you set in config.json earlier.
}`

### 5. Install Node Dependencies
Go to the folder where server.js is, right click and select `Open In Terminal`
In the terminal type `npm install` and press enter.

### Start server as a service
In the command promt window where you ran npm install run this command: `nssm install TP_ToastNotifications`
It will ask for perms click allow.
Then for Path: Select where your node.exe is installed (Usuall `"C:\Program Files\nodejs\node.exe"`)
For Startup directory: Where your server.js from the folder you downloaded from here is.
Arguments: `server.js`

Then click `Install server`

Restart your PC

### 6. Set Up TouchPortal
Add a webview to the page you want the notifications to be shown.
I used 3x2 for the size on a 7x4 page, this resolution worked for me
Set the webview URL to http://<IPv4_ADDRESS>:3000/index.html //Make sure you change <IPv4_Address> to your IPv4 Address you got from the command prompt earlier

### Usage

Notifications from PushBullet or Forward SMS will now appear as toast notifications on your TouchPortal tablet.

Customize sounds by replacing notification.mp3 in the sounds/ folder. //Must still be called notification.mp3
 - NOTE: Sounds will only play if you click inside the webview windows atleast once... I used the ADB plugin to automatically touch the screen in that area when I change to the page I have it on.

### Troubleshooting
- Ensure your phone and PC are on the same local network.
