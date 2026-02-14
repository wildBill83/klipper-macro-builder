# Klipper Macro Builder - Deployment Guide

## Quick Start (GitHub Pages - 5 Minutes)

### What You Need
- **ONLY** the `index.html` file (that's it!)
- A free GitHub account

### Step-by-Step Instructions

1. **Download the File**
   - Download `index.html` from this chat

2. **Create GitHub Account** (if you don't have one)
   - Go to https://github.com
   - Click "Sign up" and follow the prompts

3. **Create New Repository**
   - Click the "+" icon (top right) → "New repository"
   - Repository name: `klipper-macro-builder`
   - Description: "Visual Klipper macro generator"
   - Make it **Public** ✓
   - Check "Add a README file" ✓
   - Click "Create repository"

4. **Upload the File**
   - In your new repository, click "Add file" → "Upload files"
   - Drag `index.html` into the upload area
   - Scroll down, click "Commit changes"

5. **Enable GitHub Pages**
   - Click "Settings" (top navigation bar)
   - Click "Pages" in the left sidebar
   - Under "Branch", select **"main"**
   - Click "Save"
   - **WAIT 2-3 MINUTES** (GitHub needs time to build)

6. **Get Your URL**
   - Refresh the Pages settings page
   - You'll see a green box with: "Your site is published at https://YOUR-USERNAME.github.io/klipper-macro-builder/"
   - Click the URL to test it!

### Example URLs
If your GitHub username is "john3dprinter", your site will be at:
```
https://john3dprinter.github.io/klipper-macro-builder/
```

---

## Alternative: Netlify (Even Easier!)

1. Go to https://app.netlify.com/drop
2. Drag the `index.html` file onto the page
3. Done! You get an instant URL like: `https://random-name-123.netlify.app`

---

## Alternative: Vercel

1. Go to https://vercel.com
2. Sign up (free)
3. Click "Add New..." → "Project"  
4. Upload the `index.html` file
5. Click "Deploy"
6. Get your URL!

---

## Testing Locally (Before Deploying)

### Method 1: Direct Open
- Double-click `index.html`
- It should open in your default browser
- If you see a blank page, try Method 2

### Method 2: Local Server (Recommended)

**Using Python** (Mac/Linux):
```bash
# Navigate to the folder with index.html
cd ~/Downloads

# Start server
python3 -m http.server 8000

# Open browser to: http://localhost:8000
```

**Using Python** (Windows):
```cmd
cd C:\Users\YourName\Downloads
python -m http.server 8000
```

**Using VS Code**:
1. Install "Live Server" extension
2. Right-click `index.html` → "Open with Live Server"

---

## Troubleshooting

### Blank White Page
- **Wait 3-5 minutes** after enabling GitHub Pages
- Hard refresh: `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)
- Check the URL is correct: ends with `.github.io/klipper-macro-builder/`

### 404 Error
- Make sure you selected the "main" branch in Pages settings
- Make sure the file is named exactly `index.html` (lowercase)
- Wait a few more minutes

### Icons Not Showing
- Check your internet connection (icons load from CDN)
- Try a different browser
- Clear browser cache

---

## Updating Your Site

To update after deployment:

1. Go to your GitHub repository
2. Click on `index.html`
3. Click the pencil icon (Edit)
4. Make changes or paste new version
5. Click "Commit changes"
6. Wait 1-2 minutes for the site to rebuild

---

## Custom Domain (Optional)

Want a custom domain like `macros.yourname.com`?

1. Buy a domain (Namecheap, Google Domains, etc.)
2. In your repository Settings → Pages
3. Enter your custom domain
4. Add DNS records at your domain provider:
   ```
   Type: CNAME
   Name: macros (or www)
   Value: YOUR-USERNAME.github.io
   ```

---

## Features

✅ **100% Free** - No hosting costs
✅ **No Backend Needed** - Pure frontend
✅ **Mobile Friendly** - Works on phones/tablets  
✅ **Fast** - Loads in seconds
✅ **No Database** - Everything in browser
✅ **Privacy** - Your settings never leave your device

---

## Browser Support

- ✅ Chrome/Edge (Recommended)
- ✅ Firefox
- ✅ Safari
- ✅ Mobile browsers
- ⚠️ Internet Explorer (Not supported)

---

## Need Help?

1. Check the URL is correct
2. Wait 3-5 minutes after setup
3. Try incognito/private mode
4. Clear browser cache
5. Try a different browser

---

## Share Your Site

Once deployed, share the URL with:
- 3D printing forums
- Discord servers
- Reddit (r/klippers)
- Your friends!

---

Made for the Klipper community 🚀
