# Bluetooth Troubleshooting Guide

## Current Issue
The keyboard only shows as connected in Windows when the left side is plugged in via USB. This means it's using USB HID, not Bluetooth.

## How to Test True Bluetooth Connection

### 1. Output Selection
ZMK keyboards can switch between USB and Bluetooth output. To force Bluetooth:
- **With keyboard plugged in via USB**, press the output selection key combo (check your keymap)
- Common output selection combos:
  - `&out OUT_BLE` - Switch to Bluetooth output
  - `&out OUT_USB` - Switch to USB output
  - `&out OUT_TOG` - Toggle between USB and Bluetooth

### 2. Test Wireless Operation
1. Make sure both halves have charged batteries
2. Flash both halves with the latest firmware
3. Perform settings reset on BOTH halves
4. Connect left half via USB initially
5. Pair with computer via Bluetooth
6. **Important**: Press output toggle to switch to Bluetooth mode
7. Unplug USB cable - keyboard should continue working wirelessly

### 3. Check Your Keymap
Look in your `totem.keymap` file for output controls. You may need to add them if missing:
```
&out OUT_BLE  // Force Bluetooth output
&out OUT_USB  // Force USB output
&out OUT_TOG  // Toggle between them
```

### 4. Power Issues
If the keyboard disconnects when unplugged:
- Check battery connections
- Ensure batteries are charged
- The XIAO BLE has a small red LED that shows charging status

### 5. Split Communication
If only one half works wirelessly:
- Ensure both halves completed settings reset
- Left half must be the central (as configured)
- Both halves need good batteries

## Configuration Applied
- Removed mouse/pointing features (save power/memory)
- Added connection stability settings
- Set proper output priorities
- Configured for battery operation

## Next Steps
1. Flash this new firmware
2. Do settings reset on BOTH halves
3. Test with batteries in both halves
4. Check/add output selection keys in your keymap
5. Explicitly switch to Bluetooth output mode