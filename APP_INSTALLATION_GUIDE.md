# App Installation Guide - Beet Anything PWA

## What is a PWA?

Beet Anything is a **Progressive Web App (PWA)** - a modern web application that can be installed on your device like a native app. Once installed, it offers:

✅ **Works Offline** - Use without internet connection  
✅ **Faster Loading** - Instant startup from cache  
✅ **App Icon** - Appears on your home screen/desktop  
✅ **Fullscreen Mode** - No browser bars  
✅ **Automatic Updates** - Always up-to-date  
✅ **Less Data Usage** - Only downloads once  

---

## Installation Methods

### 📱 iPhone / iPad (iOS)

**Requirements:**
- iOS 11.3 or newer
- Safari browser (PWA installation only works in Safari!)

**Step-by-Step:**

1. **Open Safari**
   - Open Beet Anything in Safari browser
   - ⚠️ Chrome/Firefox don't support PWA installation on iOS

2. **Tap Share Button**
   - Tap the Share icon (□↑) at the bottom of Safari
   - It's the square with an arrow pointing up

3. **Find "Add to Home Screen"**
   - Scroll down in the share menu
   - Tap "Add to Home Screen"

4. **Customize Name (Optional)**
   - The app name will be "Beet Anything"
   - You can edit it if you want
   - The app icon will show a 🌱 plant emoji

5. **Add**
   - Tap "Add" in the top right
   - The app icon will appear on your home screen

6. **Launch App**
   - Tap the icon to open
   - App opens in fullscreen without Safari UI
   - Works like a native app

**Verification:**
- ✅ App icon visible on home screen
- ✅ No Safari address bar when opening
- ✅ Install button disappeared in the app

---

### 🤖 Android (Chrome / Samsung Internet)

**Requirements:**
- Android 5.0 or newer
- Chrome, Edge, or Samsung Internet browser

**Method 1: Automatic Prompt (Recommended)**

1. **Open App in Chrome**
   - Navigate to Beet Anything URL
   - Wait a few seconds

2. **Install Prompt Appears**
   - A banner appears at the bottom
   - Says "Install Beet Anything"

3. **Tap "Install"**
   - Confirm in the dialog
   - App will be installed

**Method 2: Manual Installation**

1. **Open Chrome Menu**
   - Tap the three dots (⋮) in the top right

2. **Select "Install app"**
   - Or "Add to Home screen"
   - Depending on your Chrome version

3. **Confirm**
   - Tap "Install" in the dialog
   - App will be added to your home screen

4. **Launch App**
   - Find app in app drawer
   - Tap to open
   - Runs in fullscreen

**Verification:**
- ✅ App in app drawer
- ✅ Opens fullscreen (no Chrome UI)
- ✅ Appears in recent apps
- ✅ Install button gone from app

---

### 💻 Desktop (Windows / Mac / Linux)

**Supported Browsers:**
- Chrome
- Edge
- Opera
- Brave

**Note:** Firefox doesn't support PWA installation

**Method 1: Address Bar Icon**

1. **Open App**
   - Navigate to Beet Anything URL in Chrome/Edge

2. **Look for Install Icon**
   - Small ⊕ icon appears in address bar
   - On the right side

3. **Click Icon**
   - Click the ⊕ icon
   - Install dialog appears

4. **Install**
   - Click "Install"
   - App window opens

**Method 2: Browser Menu**

1. **Open Browser Menu**
   - Click three dots (⋮) in top right
   - In Chrome or Edge

2. **Find "Install Beet Anything"**
   - Or "Apps" → "Install this site as an app"
   - Option depends on browser version

3. **Install**
   - Click to install
   - App window opens

4. **Pin to Taskbar (Optional)**
   - Right-click app in taskbar
   - Select "Pin to taskbar"

**Verification:**
- ✅ App in Start Menu (Windows) or Applications (Mac)
- ✅ Opens in own window (not browser tab)
- ✅ App icon in taskbar
- ✅ Install button disappeared

---

## After Installation

### What Changes?

**Before Installation:**
- Opens in browser tab
- Browser address bar visible
- Browser bookmarks/menu visible
- Install button visible in app

**After Installation:**
- Opens in standalone window
- No browser UI
- Fullscreen app experience
- Install button automatically hidden
- Faster loading (cached)

### Using the Installed App

**Opening:**
- **iOS**: Tap icon on home screen
- **Android**: Tap in app drawer or home screen
- **Desktop**: Click in Start Menu/Applications

**Updating:**
- App updates automatically
- No action needed from you
- Always latest version when online

**Uninstalling:**
- **iOS**: Long-press icon → "Remove App"
- **Android**: Long-press icon → "Uninstall"
- **Desktop**: Right-click in Start Menu → "Uninstall"

### Data After Installation

**Important:** Installing as PWA doesn't change your data!

- ✅ All existing data preserved
- ✅ Same LocalStorage
- ✅ All beds and plantings intact
- ✅ Language setting maintained
- ✅ Year and wishlist preserved

**However:** Uninstalling the PWA will delete the data!
- Always export your data before uninstalling
- Keep regular backups (monthly recommended)

---

## Troubleshooting

### Install Button Doesn't Appear

**Possible Causes:**

1. **Already Installed**
   ```
   Check if app is already installed:
   - iOS: Look for icon on home screen
   - Android: Check app drawer
   - Desktop: Check Start Menu/Applications
   ```

2. **Wrong Browser**
   ```
   iOS: Must use Safari (not Chrome/Firefox)
   Android: Use Chrome, Edge, or Samsung Internet
   Desktop: Use Chrome, Edge, or Opera
   ```

3. **Not HTTPS**
   ```
   PWAs require HTTPS connection
   Check URL starts with https://
   Local file:// won't work for PWA
   ```

4. **Browser Too Old**
   ```
   Update your browser to latest version:
   iOS: Update iOS to 11.3+
   Android: Update Chrome
   Desktop: Update Chrome/Edge
   ```

### Can't Install on iOS

**Solution:**

1. Make sure you're using Safari (not Chrome)
2. Check iOS version (must be 11.3+)
3. Try these steps:
   ```
   - Close all Safari tabs
   - Clear Safari cache
   - Restart iPhone
   - Try installation again
   ```

### App Doesn't Work Offline

**Solution:**

1. **Open app with internet first**
   - Service Worker needs to download files
   - First visit requires connection

2. **Check Service Worker registration**
   - Open app in browser
   - Open DevTools (F12)
   - Go to Application tab
   - Check Service Workers section

3. **Clear cache and reinstall**
   ```
   1. Uninstall PWA
   2. Clear browser cache
   3. Visit site with internet
   4. Install again
   ```

### Data Lost After Reinstalling

**Why:** Uninstalling PWA clears LocalStorage

**Prevention:**
```
ALWAYS export your data before:
- Uninstalling the app
- Clearing browser data
- Updating iOS/Android
- Switching devices
```

**Recovery:**
- Import your last export file
- If no backup exists, data is unrecoverable

---

## Hosting for Installation

To install Beet Anything as a PWA, it must be hosted on a web server with HTTPS.

### Option 1: GitHub Pages (Free)

```bash
1. Create GitHub account
2. Create new repository
3. Upload beet-anything.html
4. Rename to index.html
5. Enable GitHub Pages in settings
6. Visit: https://username.github.io/repo-name
```

**Advantages:**
- Free
- Automatic HTTPS
- Easy updates (git push)

### Option 2: Netlify (Free)

```bash
1. Create Netlify account
2. Drag & drop HTML file
3. Rename to index.html
4. Get URL: https://beet-anything.netlify.app
```

**Advantages:**
- Free
- Automatic HTTPS
- Custom domain support
- Instant deployment

### Option 3: Vercel (Free)

```bash
1. Create Vercel account
2. Import from GitHub
3. Auto-deploys on push
4. Get URL: https://beet-anything.vercel.app
```

**Advantages:**
- Free
- Automatic HTTPS
- Git integration
- Edge network (fast worldwide)

### Option 4: Own Server

**Requirements:**
- HTTPS certificate (Let's Encrypt)
- Web server (Apache, Nginx)
- Domain name

**Upload:**
```bash
# Via FTP/SFTP
Upload beet-anything.html to web root
Rename to index.html
Ensure HTTPS is configured
```

---

## Multi-Device Usage

### Same Data on Multiple Devices?

**No automatic sync** - Each device has separate data.

**To share data between devices:**

1. **On Device 1:**
   - Open app
   - Click "💾 Export Data"
   - Save JSON file
   - Upload to cloud (Dropbox, Google Drive, etc.)

2. **On Device 2:**
   - Open app
   - Download JSON file from cloud
   - Click "📂 Import Data"
   - Select JSON file

3. **Result:**
   - Both devices now have same data
   - Changes are NOT automatically synced
   - Repeat export/import to keep in sync

### Recommended Workflow (Multi-Device)

```
1. Choose "main" device (e.g., laptop)
2. Do most planning on main device
3. Export weekly
4. Import on other devices as needed
5. Make small changes on mobile
6. Export from mobile before big changes on laptop
```

---

## Advanced: Install from Local File

### For Development / Testing

**Requirements:**
- Local web server
- HTTPS (self-signed certificate OK for testing)

**Option 1: Python HTTP Server**

```bash
# Create self-signed certificate
openssl req -x509 -newkey rsa:4096 -nodes -out cert.pem -keyout key.pem -days 365

# Start HTTPS server (Python 3)
python3 -m http.server --bind localhost 8000 --protocol=https

# Visit
https://localhost:8000/beet-anything.html
```

**Option 2: Node.js HTTP Server**

```bash
# Install http-server
npm install -g http-server

# Start with SSL
http-server -S -C cert.pem -K key.pem

# Visit
https://localhost:8080/beet-anything.html
```

**Note:** Browsers will warn about self-signed certificate. This is OK for testing.

---

## Frequently Asked Questions

### Do I need to install it?

**No** - You can use Beet Anything in the browser without installing.

**But installing gives you:**
- Faster loading
- Offline access
- Fullscreen experience
- App-like feel

### Does it use internet data?

**First visit:** Yes, downloads ~105 KB
**After installation:** No, runs from cache
**Updates:** Only when we release new version
**Total data usage:** < 200 KB

### Will it work without internet?

**Yes** - After first visit, everything works offline:
- Planning
- Editing
- Suggestions algorithm
- Export/import
- Language switching

**Only requires internet for:**
- First installation
- Loading Inter font (first time)
- Updating to new version

### Can I use it on multiple phones?

Yes, but data doesn't sync automatically. See "Multi-Device Usage" above.

### Is my data safe?

**Privacy:**
- 100% local storage
- No server uploads
- No tracking
- No analytics

**Security:**
- Data stays on your device
- HTTPS encryption (when hosted)
- No passwords/accounts needed

**Backup responsibility is yours:**
- Export regularly
- Keep backups in cloud
- Data lost if app uninstalled

### How do I update the app?

**Automatic** - No action needed:
- App checks for updates when online
- Downloads updates in background
- Updates on next launch

**Manual check:**
```
1. Close app completely
2. Connect to internet
3. Open app
4. New version loads automatically
```

### Can I install on work computer?

**Usually yes** - It's just a website:
- No admin rights needed
- Doesn't modify system
- Can uninstall anytime

**Check with IT department if:**
- Company has strict policies
- Network blocks external sites
- You need approval for software

---

## Additional Resources

### Getting Help

- **Installation Issues**: Check troubleshooting section above
- **App Usage**: See README.md
- **Development**: See BEET_ANYTHING_RESUME.md
- **Mobile Optimization**: See MOBILE_OPTIMIZATION.md

### External Resources

- **PWA Documentation**: https://web.dev/progressive-web-apps/
- **Browser Support**: https://caniuse.com/serviceworkers
- **Apple PWA Guide**: https://developer.apple.com/documentation/webkit/progressive_web_apps

---

**Document Version**: 1.1  
**Last Updated**: February 2025  
**Product**: Beet Anything v1.1 i18n  
**Platforms**: iOS, Android, Desktop (Windows/Mac/Linux)
