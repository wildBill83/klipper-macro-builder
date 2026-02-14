# Klipper Macro Builder

A visual tool for building production-ready Klipper START_PRINT and END_PRINT macros with material-specific settings, nozzle cleaning, bed mesh calibration, and more.

## Features

- **Material-Specific Settings**: Heat soak times, chamber temps, pressure advance, velocity limits, and Z offsets for PLA, PETG, ABS, ASA, TPU, Nylon, and PC
- **Bed Leveling**: QGL, Z-tilt, bed mesh calibration with adaptive mesh support
- **Bed Thermal Expansion Check**: For printers like Sovol SV08 to verify bed stability
- **Nozzle Cleaning**: Built-in brush patterns (X or Y orientation) or custom macro support
- **Chamber Control**: Support for active heaters or passive temperature monitoring
- **Carbon Filtration**: Three modes - during print, cooldown, and post-print
- **Sensorless Homing Safety**: Automatic acceleration reset to prevent false triggers
- **Collapsible UI**: Clean, organized interface with expandable sections
- **_CLIENT_VARIABLE Support**: Centralized configuration without editing macros

## Deployment Options

### Option 1: GitHub Pages (Recommended - Free & Easy)

1. **Create a GitHub Account** (if you don't have one)
   - Go to https://github.com
   - Click "Sign up"

2. **Create a New Repository**
   - Click the "+" icon in top right → "New repository"
   - Name it: `klipper-macro-builder` (or any name you want)
   - Make it **Public**
   - Check "Add a README file"
   - Click "Create repository"

3. **Upload Files**
   - Click "Add file" → "Upload files"
   - Drag and drop these two files:
     - `index.html`
     - `klipper-macro-builder.jsx`
   - Click "Commit changes"

4. **Enable GitHub Pages**
   - Go to repository Settings (gear icon)
   - Scroll down to "Pages" in left sidebar
   - Under "Source", select "main" branch
   - Click "Save"
   - Wait 1-2 minutes

5. **Access Your Site**
   - Your site will be at: `https://YOUR-USERNAME.github.io/klipper-macro-builder/`
   - Example: `https://johnsmith.github.io/klipper-macro-builder/`

### Option 2: Netlify (Free, Drag & Drop)

1. **Go to Netlify**
   - Visit https://www.netlify.com
   - Click "Sign up" (can use GitHub account)

2. **Deploy**
   - Click "Add new site" → "Deploy manually"
   - Drag the folder containing `index.html` and `klipper-macro-builder.jsx`
   - Wait for deployment (30 seconds)

3. **Access Your Site**
   - You'll get a URL like: `https://random-name-123456.netlify.app`
   - You can customize the name in Site settings

### Option 3: Vercel (Free, Git-based)

1. **Go to Vercel**
   - Visit https://vercel.com
   - Click "Sign Up" (use GitHub account)

2. **Import Repository**
   - Click "Add New..." → "Project"
   - Import your GitHub repository
   - Click "Deploy"

3. **Access Your Site**
   - You'll get a URL like: `https://klipper-macro-builder.vercel.app`

### Option 4: Self-Hosted (Your Own Server)

1. **Upload Files**
   - Upload `index.html` and `klipper-macro-builder.jsx` to your web server
   - Place them in the same directory

2. **Access**
   - Visit: `http://your-domain.com/index.html`

## Local Testing

To test locally before deploying:

1. Open `index.html` in a web browser
2. That's it! Everything runs in the browser.

**Note**: Some browsers may block local file loading. If you see errors, use one of these:

**Option A - Python Simple Server:**
```bash
# In the folder with your files, run:
python3 -m http.server 8000

# Then open: http://localhost:8000
```

**Option B - VS Code Live Server:**
- Install "Live Server" extension in VS Code
- Right-click `index.html` → "Open with Live Server"

## Usage

1. **Configure Material Settings**
   - Expand "Material-Specific Settings" section
   - Adjust heat soak times, chamber temps, and motion settings

2. **Select Options**
   - Enable/disable features in each section
   - Configure coordinates for brush, bed warp check, etc.

3. **Copy Macros**
   - Click "Copy to Clipboard"
   - Paste into your `printer.cfg`

4. **Configure OrcaSlicer**
   - Follow the setup instructions shown in the tool
   - Add the START_PRINT and END_PRINT calls to your slicer

## OrcaSlicer Configuration

**Machine Start G-code:**
```gcode
START_PRINT BED_TEMP=[bed_temperature_initial_layer_single] EXTRUDER_TEMP=[nozzle_temperature_initial_layer] FILAMENT_TYPE=[filament_type] CHAMBER_TEMP=[chamber_temperature] BED_TYPE=SMOOTH
```

**Machine End G-code:**
```gcode
END_PRINT
```

## Browser Compatibility

- Chrome/Edge: ✅ Fully supported
- Firefox: ✅ Fully supported  
- Safari: ✅ Fully supported
- Mobile browsers: ✅ Responsive design

## Technical Details

- **Frontend Only**: No backend required, runs entirely in browser
- **No Data Collection**: Everything stays in your browser
- **Offline Capable**: Works without internet after initial load (if cached)

## License

Free to use and modify for personal and commercial use.

## Credits

Created for the Klipper 3D printing community.

## Support

For issues or feature requests, please open an issue on the GitHub repository.
