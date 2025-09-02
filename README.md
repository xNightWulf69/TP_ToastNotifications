# TouchPortal WebView Toast Notifications

A real-time notification system that displays toast notifications on your TouchPortal tablet from your phone using TouchPortal's WebView feature.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-green.svg)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey.svg)

## 🌟 Features

- **Real-time notifications**: Instant display of phone notifications on your TouchPortal tablet
- **Customizable**: Replace notification sounds with your own audio files
- **Toast-style UI**: Clean, non-intrusive notification display

## 📋 Prerequisites

- **Hardware**: Windows PC and TouchPortal tablet on the same local network
- **Software**: [Node.js](https://nodejs.org/) (v18 or higher)
- **Mobile Apps**: PushBullet and Forward SMS (installation covered below)

## 🚀 Installation

### Step 1: Setup the Server

1. **Clone or download this repository**
   ```bash
   git clone https://github.com/xNightWulf69/TP_ToastNotifications.git
   cd TP_ToastNotifications
   ```
   
   *Or download as ZIP from GitHub: Code → Download ZIP → Then extract the folder to where you want it*

2. **Install Node.js dependencies**
   In the folder you extracted, right click a blank space in the folder and clock `Open in Terminal`
   In the terminal run:
   ```bash
   npm install
   ```

### Step 2: Configure PushBullet

1. Create a [PushBullet](https://www.pushbullet.com) account
2. Navigate to **My Account → Settings → Create Access Token**
3. Copy the generated access token

### Step 3: Configure the Application

1. Open `config.json` in your preferred text editor
2. Update the following settings:
   ```json
{
  "PUSHBULLET_ACCESS_TOKEN": "YourTokenHere",
  "SMS_SECRET": "Secret",
  "appMap": {
    "whatsapp": { "color": "#25D366" },
    "messenger": { "color": "#0084FF" },
    "snapchat": { "color": "#FFFC00" },
    "pushbullet": { "color": "#4ab367" },
    "discord": { "color": "#5d6feb" },
    "instagram": { "color": "#fe089f" },
    "x": { "color": "#ffffff" },
    "gmail": { "color": "#ce3c30" },
    "outlook": { "color": "#0078D4" },
    "facebook": { "color": "#1877F2" },
    "youtube": { "color": "#FF0000" },
    "uber eats": { "color": "#06c167" }
  }
}
   ```
The SMS_SECRET can be whatever you want, but needs to be used later on your phone.


### 🎨 Customize Notification Colors

The `appMap` section allows you to customize the toast notification border color for different apps:

- **App names** should be lowercase and match the notification source
- **Colors** use hex color codes (e.g., `#25D366` for WhatsApp green)
- **Add new apps** by adding entries like: `"appname": { "color": "#hexcode" }`
- **Remove apps** you don't want colored by deleting their entries

**Example**: To add TikTok with a pink border:
```json
"tiktok": { "color": "#FF0050" }
```


### Step 4: Get Your PC's IP Address

Open Command Prompt and run:
```cmd
for /f "tokens=2 delims=:" %a in ('ipconfig ^| find "IPv4"') do @echo %a
```
**Save this IP address** - you'll need it for the next steps.

### Step 5: Configure Mobile Apps

#### PushBullet Setup
1. Install **PushBullet: SMS on PC and more** from your app store
2. Login with the same Google account used in Step 2
3. Grant all requested permissions during setup
4. Navigate to **Mirroring** and enable **Notification Mirroring**

#### Forward SMS Setup
1. Install **Forward SMS** by Point Dume
2. Create a new rule: **Add rule → Basic Rule**
3. Set forwarding destination to **URL**
4. Configure the URL settings:
   - **Method**: `POST`
   - **URL**: `http://YOUR_IP_ADDRESS:3000/sms` (replace `YOUR_IP_ADDRESS` with the IP from Step 4)
   - **Body**:
     ```json
     {
       "sender": "{sender}",
       "message": "{msg}",
       "secret": "your_sms_secret_from_config"
     }
     ```

### Step 6: Install as Windows Service

1. Install the service manager:
   In the terminal used to run npm install run:
   ```cmd
   nssm install TP_ToastNotifications
   ```

2. Configure the service (when the dialog opens):
   - **Path**: `C:\Program Files\nodejs\node.exe` (or your Node.js installation path)
   - **Startup directory**: Path to your project folder containing `server.js`
   - **Arguments**: `server.js`

3. Click **Install Service**
4. **Restart your PC** to start the service

### Step 7: Setup TouchPortal WebView

1. In TouchPortal, add a **WebView** element to your desired page
2. **Recommended size**: 3×2 grid on a 7×4 page
3. Set the WebView URL to: `http://YOUR_IP_ADDRESS:3000/index.html`
4. Replace `YOUR_IP_ADDRESS` with your PC's IP address from Step 4

## 🎵 Audio Configuration

### Custom Notification Sounds
- Replace `sounds/notification.mp3` with your preferred audio file
- **Important**: Keep the filename as `notification.mp3`
- **Audio Limitation**: Sounds only play after clicking inside the WebView at least once
  - *Tip: Use the ADB plugin to auto-touch the WebView area when switching pages*

## 🔧 Usage

Once configured, notifications from PushBullet or Forward SMS will automatically appear as toast notifications on your TouchPortal tablet.

### Testing Your Setup
1. Send yourself a test message through PushBullet
2. Check if the notification appears on your TouchPortal tablet
3. Verify audio playback (remember to click the WebView first)

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| **No notifications appearing** | Ensure your phone and PC are on the same local network |
| **Service not starting** | Check that Node.js path is correct in NSSM configuration |
| **Forward SMS not working** | Verify the URL and secret match your config.json settings |
| **No sound playing** | Click inside the WebView area once to enable audio |
| **Connection refused** | Confirm the server is running on port 3000 |

### Common Network Issues
- Check Windows Firewall settings for port 3000
- Ensure your router allows local network communication
- Try temporarily disabling antivirus software to test connectivity

## 📁 Project Structure

```
TP_ToastNotifications/
├── server.js           # Main server application
├── index.html          # WebView interface
├── config.json         # Configuration file
├── package.json        # Node.js dependencies
├── sounds/
│   └── notification.mp3 # Default notification sound
└── README.md           # This file
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⭐ Acknowledgments

- TouchPortal team for the excellent tablet interface
- PushBullet for their notification API
- Forward SMS developers for SMS forwarding capabilities

---

**Found this helpful?** Give it a ⭐ and share with other TouchPortal users!
