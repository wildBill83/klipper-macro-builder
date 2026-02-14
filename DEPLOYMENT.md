# Deploy to GitHub Pages - Simple Instructions

## What You Need

- GitHub account (free at github.com)
- The `index.html` file (download from this chat)

## Step-by-Step Deployment

### 1. Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: `klipper-macro-builder` (or whatever you want)
3. Description: `Visual tool for Klipper START_PRINT and END_PRINT macros`
4. Select **Public**
5. Check ✓ **Add a README file**
6. Click **Create repository**

### 2. Upload the File

1. In your new repository, click **Add file** → **Upload files**
2. Drag the `index.html` file into the upload area
3. Scroll down and click **Commit changes**

### 3. Enable GitHub Pages

1. Click **Settings** (top menu bar)
2. Click **Pages** in the left sidebar
3. Under "Build and deployment":
   - **Source**: Deploy from a branch
   - **Branch**: main
   - **Folder**: / (root)
4. Click **Save**

### 4. Wait and Access

1. **Wait 2-3 minutes** for GitHub to build your site
2. Refresh the Pages settings page
3. You'll see: "Your site is live at `https://YOUR-USERNAME.github.io/klipper-macro-builder/`"
4. Click the URL to visit your site!

## Your URL Will Be

```
https://YOUR-USERNAME.github.io/klipper-macro-builder/
```

Replace `YOUR-USERNAME` with your actual GitHub username.

Example: If your username is `john3dprinter`, your URL is:
```
https://john3dprinter.github.io/klipper-macro-builder/
```

## Share Your Site

Once deployed, anyone can access your tool at that URL!

Share it on:
- 3D printing forums
- Reddit (r/klippers, r/3Dprinting)
- Discord servers
- Facebook groups

## Troubleshooting

### Blank Page After 3 Minutes

1. **Hard refresh**: Press `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)
2. **Try incognito mode**: Open in private/incognito window
3. **Check the URL**: Make sure it ends with `/klipper-macro-builder/` (with the slash)
4. **Wait longer**: Sometimes takes 5 minutes on first deploy

### Still Not Working?

1. Make sure the file is named exactly `index.html` (all lowercase)
2. Make sure you selected the **main** branch (not master)
3. Make sure the repository is **Public** (not Private)
4. Try a different browser

### See Errors in Browser Console?

1. Press F12 to open browser console
2. If you see Tailwind warning - **ignore it**, the site still works
3. If you see other errors, delete the repository and start fresh

## Updating Your Site

To update after making changes:

1. Go to your repository
2. Click on `index.html`
3. Click the pencil icon (Edit)
4. Replace with new version
5. Click **Commit changes**
6. Wait 1-2 minutes for update

## Alternative: Netlify Drop (Even Easier!)

If GitHub Pages is giving you trouble:

1. Go to https://app.netlify.com/drop
2. Drag `index.html` onto the page
3. Get instant URL like `https://random-name-123.netlify.app`
4. Done in 30 seconds!

---

That's it! The tool will be live and accessible to anyone with the URL.
