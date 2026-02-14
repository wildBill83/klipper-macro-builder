# Klipper Macro Builder - Complete User Guide

## 📖 Table of Contents

1. [Getting Started](#getting-started)
2. [Material-Specific Settings](#material-specific-settings)
3. [Bed Leveling Options](#bed-leveling-options)
4. [Nozzle Cleaning](#nozzle-cleaning)
5. [Heating Configuration](#heating-configuration)
6. [Purge & Prime](#purge--prime)
7. [Advanced Settings](#advanced-settings)
8. [END_PRINT Options](#end_print-options)
9. [OrcaSlicer Setup](#orcaslicer-setup)
10. [Troubleshooting](#troubleshooting)

---

## Getting Started

### First Time Setup

1. **Open the tool** (in this Claude conversation, scroll up to find the blue "Klipper Macro Builder" card)
2. **Configure Material Settings** (expand the "Material-Specific Settings" section)
3. **Select features** you want in each section
4. **Copy the generated macro** (click "Copy to Clipboard")
5. **Paste into your `printer.cfg`**
6. **Configure your slicer** (see [OrcaSlicer Setup](#orcaslicer-setup))

---

## Material-Specific Settings

This table configures behavior for each filament type (PLA, PETG, ABS, ASA, TPU, Nylon, PC).

### Heat Soak (minutes)
**What it does:** Time to wait after bed reaches temperature for thermal expansion to stabilize

**Recommended values:**
- PLA: 0 (no soak needed)
- PETG: 3-5 minutes
- ABS/ASA: 10-15 minutes
- Nylon/PC: 15-20 minutes
- TPU: 0

**Why:** High-temp materials need time for the bed to fully heat through and expand evenly

### Chamber Temp (°C)
**What it does:** Target chamber temperature (if you have chamber heating/monitoring)

**Recommended values:**
- PLA/PETG/TPU: 0 (disabled)
- ABS/ASA: 40-50°C
- Nylon: 50-60°C  
- PC: 60-70°C

**How it works:**
- If you enable "Enable Chamber Temperature Control" in Heating section
- Macro uses OrcaSlicer's CHAMBER_TEMP parameter if provided (>0)
- Otherwise falls back to these material defaults
- If you have an active chamber heater, check "Has Active Chamber Heater"

### Z Offset - Smooth vs Textured
**What it does:** Automatically adjusts Z height based on build plate type

**Example values:**
- Smooth PEI: 0.00mm (baseline)
- Textured PEI: +0.03 to +0.06mm (textured is "taller")

**How to use:**
1. Calibrate Z offset on your smooth plate, set to 0.00
2. Switch to textured plate, do a test print
3. If nozzle too high, increase value (e.g., +0.04)
4. Enable "Bed Type Z Offset" in Advanced section
5. Add `BED_TYPE=SMOOTH` or `BED_TYPE=TEXTURED` to your slicer start gcode

### Pressure Advance
**What it does:** Compensates for filament compression in the extruder

**⚠️ Warning:** Most modern slicers (OrcaSlicer, PrusaSlicer, SuperSlicer) already handle this per-filament. Only enable if you prefer macro-based control.

**Typical values:**
- PLA: 0.04-0.06
- PETG: 0.06-0.09
- ABS: 0.03-0.05
- TPU: 0.00-0.01

**How to calibrate:** Use Klipper's pressure advance calibration pattern

### Velocity & Acceleration
**What it does:** Sets speed limits per material

**⚠️ Warning:** Slicers usually handle this better. Only enable for macro-based control.

**Typical values:**
- PLA/ABS: 300mm/s velocity, 3000mm/s² accel
- PETG: 250mm/s, 2500mm/s²
- TPU: 60mm/s, 1000mm/s²

### SCV (Square Corner Velocity)
**What it does:** Controls cornering speed (like "jerk" in Marlin)

**Typical value:** 0.005 for most materials

**Effect:**
- Lower (0.001-0.003): Smoother corners, slower print
- Higher (0.008-0.015): Sharper corners, faster print

---

## Bed Leveling Options

### Home Y Before X
**When to use:** Bed-slinger printers (moving bed on Y axis) like Ender 3, CR-10

**Why:** Prevents crashes by moving the bed forward before the nozzle moves side-to-side

**Leave unchecked for:** CoreXY, Voron, or other non-bed-slinger designs

### Bed Thermal Expansion Check
**When to use:** Printers with aluminum beds that warp when heating (Sovol SV08, Ender 3 S1, etc.)

**How it works:**
1. After heat soak, probes same spot multiple times (e.g., bed center)
2. Waits between probes (default: 60 seconds)
3. Calculates variance between probe readings
4. If variance > tolerance, shows warning
5. Prevents printing on unstable bed

**Configuration:**
- **Probe X/Y:** Center of bed (e.g., X=150, Y=150 for 300mm bed)
- **Probe Count:** 3-5 probes recommended
- **Interval:** 30-90 seconds between probes
- **Tolerance:** 0.01mm = ±0.01mm variance allowed

**Example:** 
- Probe 1: Z=0.250mm
- Probe 2: Z=0.255mm (60s later)  
- Probe 3: Z=0.256mm (60s later)
- Variance: 0.006mm ✅ (bed is stable)

### Load Saved Bed Mesh
**What it does:** Loads a pre-calibrated mesh from memory

**When to use:** You've already calibrated your mesh and saved it

**Mesh Profile Name:** The name you saved it as (default: "default")

**To save a mesh:** Run `BED_MESH_CALIBRATE` then `BED_MESH_PROFILE SAVE=my_name`

### Calibrate Bed Mesh
**What it does:** Probes the bed and creates a new mesh

**When to use:** First print of the day, or if bed may have changed

**Adaptive Mesh:** Only probes the area where your print will be (faster, more accurate for that print)

### QGL vs Z-Tilt
**Mutually exclusive** - choose one:

**Quad Gantry Level (QGL):**
- For: Voron 2.x, Trident (4 Z motors)
- Does: Levels the gantry to the bed
- When: Every print or when changing bed surface

**Z-Tilt:**
- For: Printers with multiple Z motors (not QGL setup)
- Does: Adjusts Z motors to level bed plane
- When: Every print or after any mechanical change

---

## Nozzle Cleaning

### Enable Nozzle Brush/Cleaning
Turn this on if you have a nozzle brush or wiper installed.

### Clean Before Probing
**Recommended:** ON

**Why:** 
- Nozzle is pre-heated for probing (e.g., 150°C)
- Plastic oozes out during heat-up
- Ooze on nozzle = inaccurate Z probe readings
- Clean nozzle = accurate first layer

**When to disable:** If you clean after full heating instead

### Cleaning Method

#### Built-in Brush Pattern
Configure your brush location:

**Brush Orientation:**
- **X-axis (left-right):** Brush runs left/right, wipes along X
- **Y-axis (front-back):** Brush runs front/back, wipes along Y

**⚠️ Critical:** Choose correct orientation or you'll wipe perpendicular to brush (ineffective/damaging)

**Brush X/Y:** Start position of brush
- Example: X=50, Y=300 (back-left corner of 300mm bed)

**Brush Z:** Height when nozzle contacts brush
- Typical: Z=1.0 to Z=2.0mm
- Too low: Crashes into brush mount
- Too high: Misses bristles

**Brush Width:** Length of brush along its orientation
- X-axis brush: Width = X distance
- Y-axis brush: Width = Y distance
- Typical: 40-60mm

**Wipe Passes:** Number of back-forth cycles
- Recommended: 3-5 passes
- Light ooze: 2-3
- Heavy stringing: 5-10

**Movement pattern (X-axis example):**
```
1. Lift to Z=10mm
2. Move to brush start (X=50, Y=300)
3. Lower to brush height (Z=1.0)
4. Wipe right (X=50 → X=100)
5. Wipe left (X=100 → X=50)
6. Repeat for number of passes
7. Lift to Z=10mm
```

#### Custom Macro
If you have an existing cleaning macro (e.g., from Voron config):

1. Select "Custom Macro"
2. Enter macro name: `CLEAN_NOZZLE`
3. Make sure this macro exists in your printer.cfg

---

## Heating Configuration

### Heat Soak (material-based)
**What it does:** Waits for bed to fully heat-soak using times from Material Settings table

**How it works:**
1. Heats bed to target temperature (M190)
2. Waits for material-specific soak time
3. Example: ABS = wait 10 minutes after bed reaches 110°C

**When to disable:** PLA prints, quick prints, pre-heated printer

### Enable Chamber Temperature Control
**What it does:** Waits for chamber to reach target temperature

**How it works:**
1. Uses CHAMBER_TEMP parameter from OrcaSlicer (if > 0)
2. If CHAMBER_TEMP=0, uses material default from table
3. Waits until chamber sensor reads target temp
4. Only proceeds to print after chamber ready

**Has Active Chamber Heater:**
- **Checked:** Uses M191 to actively heat chamber (like a bed heater)
- **Unchecked:** Passively waits for temperature sensor to reach target

**When to use:** Enclosed printers with chamber heaters or monitoring (Voron, Prusa XL, custom builds)

### Nozzle Pre-Heat Temp
**What it does:** Partially heats nozzle for probing without full ooze

**Typical value:** 150-170°C

**Why:** 
- Cold nozzle = inaccurate probe offset (thermal expansion)
- Full temp = massive ooze during probing
- Pre-heat = accurate probing, minimal ooze

**Set to 0 to disable:** Probe at room temp (not recommended)

---

## Purge & Prime

### Purge Line Type

**None:** No purge (use if you have custom purge in slicer)

**Adaptive (near print):**
- Requires `ADAPTIVE_PURGE` macro (KAMP or similar)
- Purges next to the first layer of your print
- Minimal waste, no travel after purge
- **Recommended** if available

**Front Line:**
- Classic dual-line purge at front of bed
- Position: X=10, Y=10, travels 190mm in Y
- 30mm of filament extruded
- Adjust coordinates if different bed size

**Prime Blob:**
- Single stationary extrusion
- Position: X=10, Y=10
- 10mm of filament
- Quick, but may string

### Extra Prime (mm)
**What it does:** Additional extrusion after purge line

**When to use:**
- New/partial filament
- First print after filament change
- TPU or flexible materials

**Typical:** 0-5mm

---

## Advanced Settings

### Support _CLIENT_VARIABLE Overrides
**What it does:** Allows centralized configuration without editing the macro

**How to use:**
1. Enable this option
2. Create a `_CLIENT_VARIABLE` macro in printer.cfg:

```gcode
[gcode_macro _CLIENT_VARIABLE]
variable_mesh_profile: "textured_mesh"      # Override mesh name
variable_skew_profile: "my_skew"            # Override skew profile  
variable_bed_warp_x: 150                    # Override warp check position
variable_bed_warp_y: 150
variable_brush_x: 50                        # Override brush position
variable_brush_y: 300
variable_brush_z: 1.0
variable_brush_width: 50
variable_brush_orientation: "X"
gcode:
```

3. Values in `_CLIENT_VARIABLE` override the macro defaults
4. Update variables in one place instead of editing macro

**When to use:** Multiple printers, frequent config changes, shared configs

### Bed Type Z Offset
**What it does:** Auto-adjusts Z based on `BED_TYPE` parameter

**Enable this + configure Z offsets in Material Settings table**

**In your slicer start gcode:**
```gcode
START_PRINT ... BED_TYPE=SMOOTH
# or
START_PRINT ... BED_TYPE=TEXTURED
```

### Filament Type Parameter
**Always enable** - this is how the macro knows which material you're printing

**Required in slicer:** `FILAMENT_TYPE=[filament_type]`

### Auto Pressure Advance / Velocity Limits
**⚠️ Usually leave disabled** 

Slicers handle these better with per-layer control. Only enable if you:
- Use an old slicer without per-filament settings
- Prefer macro-based control for specific workflow

### Skew Correction
**What it does:** Compensates for non-square printer geometry

**When to use:** After running Klipper's skew calibration and saving a profile

**Profile name:** Whatever you saved it as (default: `my_skew_profile`)

### Initial Fan Speed (%)
**What it does:** Sets part cooling fan speed at print start

**Typical values:**
- PLA: 0% (let slicer control)
- PETG: 0-30%
- ABS/ASA: 0% (usually no fan)
- TPU: 0-50%

**Note:** Slicer will override this, so usually leave at 0

---

## END_PRINT Options

### Toolhead Parking

**Park Position:**
- **Back Center:** Middle of back (good for part removal)
- **Back Left/Right:** Corner parking
- **Front Center:** Front middle (for bed-slingers)

**Z Position:**
- **Near Max Z:** Raises Z to almost maximum height (safest)
- **+10mm Relative:** Moves Z up 10mm from current position (quick)

**Present Part:**
- Lowers bed to 80% of max Z for easy part removal
- Good for tall builds

### Retraction
**Distance:** How much to retract at end (typically 2-5mm)

**Why:** Prevents oozing after print, easier filament reload

### Cooling & Filtration

**Part Cooling Fan:**
- Turns part cooling fan to 100% after print
- Helps cool part faster
- Turn off with part cooling option

**Fan Cooldown Period:**
- Runs cooling fan for X seconds before turning off
- Helps cool part while still in enclosure

**Carbon Filter Options:**

1. **During Print (active filtration):**
   - Runs filter throughout entire print
   - Use for: ABS, ASA, Nylon (fume control)
   - Speed: 0.5 = 50% fan speed (adjustable)

2. **During Cooldown (immediate cleanup):**
   - Runs after print, during cooldown period
   - Use for: Quick air cleaning
   - Duration: 60-300 seconds typical

3. **Post-Print (extended cleaning):**
   - Runs AFTER everything else completes
   - Use for: Deep air cleaning, overnight prints
   - Duration: 300-1800 seconds (5-30 minutes)

**Which to use?**
- ABS/ASA/Nylon: All three (during + cooldown + post)
- PETG: Cooldown + post
- PLA: None or just post-print

### Power Down

**Reset Acceleration to Defaults:**
**⚠️ Important for sensorless homing printers**

**What it does:** Resets velocity/accel to safe values after print

**Why:** 
- Print may use high acceleration (3000-10000mm/s²)
- Next homing with high accel = false trigger on sensorless homing
- Reset to conservative values = reliable homing

**Default values:**
- Velocity: 300mm/s
- Accel: 3000mm/s²

**When to use:** Voron, any printer with TMC sensorless homing

**Turn Off Bed Heater:**
- Disables bed after print
- Leave unchecked if printing multiple items

**Disable Steppers (M84):**
- Turns off motors after print
- **Don't use** if you want to reprint same part (loses position)
- **Use** for one-off prints, saves electricity

**Completion Beep:**
- Makes printer beep when done
- Requires M300 support

---

## OrcaSlicer Setup

### Machine Start G-code

**Basic:**
```gcode
START_PRINT BED_TEMP=[bed_temperature_initial_layer_single] EXTRUDER_TEMP=[nozzle_temperature_initial_layer] FILAMENT_TYPE=[filament_type] CHAMBER_TEMP=[chamber_temperature]
```

**With bed type Z offset:**
```gcode
START_PRINT BED_TEMP=[bed_temperature_initial_layer_single] EXTRUDER_TEMP=[nozzle_temperature_initial_layer] FILAMENT_TYPE=[filament_type] CHAMBER_TEMP=[chamber_temperature] BED_TYPE=SMOOTH
```

Change `BED_TYPE=SMOOTH` to `BED_TYPE=TEXTURED` when using textured plate.

### Machine End G-code
```gcode
END_PRINT
```

That's it!

### Per-Filament Settings

In OrcaSlicer, you can override chamber temp per filament:
1. Go to Filament Settings
2. Find "Chamber temperature"  
3. Set desired temp (or 0 to use macro defaults)

---

## Troubleshooting

### First Layer Too High/Low
1. Check Z offset calibration
2. If using bed type Z offset, verify values in Material Settings
3. Make sure bed mesh loaded or calibrated
4. If using nozzle brush, verify it's cleaning before probing

### Bed Warp Check Keeps Failing
- Increase tolerance (try 0.02-0.05mm)
- Increase interval between probes (90-120 seconds)
- Increase heat soak time
- Check bed is truly at temp with thermal camera

### Nozzle Brush Not Working
- Verify brush orientation (X vs Y)
- Check brush Z height (too high = miss bristles)
- Confirm brush position coordinates
- Watch it in action, adjust accordingly

### Chamber Not Heating
- If passive (no heater): Wait longer, check sensor
- If active heater: Verify chamber heater configured in Klipper
- Check CHAMBER_TEMP parameter being passed from slicer

### Sensorless Homing Failing
- Enable "Reset Acceleration to Defaults"
- Lower default accel value (try 2000mm/s²)
- Verify TMC sensitivity settings

### Print Starts with Huge Ooze Blob
- Enable "Clean Before Probing"
- Add purge line
- Reduce nozzle pre-heat temp

### Macro Takes Forever
- Reduce heat soak times for faster materials (PLA = 0)
- Disable bed warp check for stable beds
- Skip chamber temp for materials that don't need it

---

## Tips & Best Practices

1. **Start Conservative:** Enable only what you need, add features gradually
2. **Test Each Feature:** Add one feature at a time, test print between changes
3. **Document Your Settings:** Take screenshots of your material settings table
4. **Different Profiles:** Generate different macros for different printer setups
5. **Version Control:** Save dated copies of your macros when making changes

---

## Example Configurations

### Simple PLA Profile (Ender 3)
- Heat soak: 0 minutes
- Chamber: Disabled
- Bed mesh: Load saved
- QGL/Z-tilt: Disabled
- Nozzle clean: Disabled
- Purge: Front line
- Carbon filter: None

### Advanced ABS Profile (Voron 2.4)
- Heat soak: 10 minutes
- Chamber: 45°C active heater
- Bed warp check: Enabled
- QGL: Enabled
- Bed mesh: Adaptive calibrate
- Nozzle clean: Enabled, before probing
- Purge: Adaptive
- Carbon filter: All three modes

### Multi-Material Setup (Prusa MK4)
- Material settings: Calibrated for all 7 materials
- Bed type Z offset: Enabled (smooth + textured plates)
- Everything else: Standard
- Saves time when switching materials

---

Need help with a specific feature? Ask in the chat!
