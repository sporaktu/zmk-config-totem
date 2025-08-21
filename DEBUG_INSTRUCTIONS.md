# Bluetooth Debug Instructions for Totem Keyboard

## How to Capture Debug Logs

### 1. Build and Flash Debug Firmware
- Commit and push the changes to trigger GitHub Actions build
- Download and flash the new firmware with debug logging enabled

### 2. Connect via USB and Capture Logs

#### Windows (PuTTY)
1. Install PuTTY if not already installed
2. Open Device Manager to find COM port number (e.g., COM3)
3. Open PuTTY:
   - Connection type: Serial
   - Serial line: COM3 (or your port)
   - Speed: 115200
4. Click "Open" and logs will appear

#### macOS/Linux (screen)
1. Find the device: `ls /dev/tty.*` or `ls /dev/ttyACM*`
2. Connect: `screen /dev/tty.usbmodem14401 115200` (adjust device name)
3. To exit screen: `Ctrl-A` then `K` then `Y`

#### Alternative: tio (recommended)
1. Install tio: `brew install tio` (macOS) or `sudo apt install tio` (Linux)
2. Connect: `tio /dev/ttyACM0` or `tio /dev/tty.usbmodem*`
3. To exit: `Ctrl-T` then `Q`

### 3. Trigger the Bluetooth Issue
1. With logging terminal open and connected
2. Try to pair with your computer via Bluetooth
3. Watch for error messages when it disconnects

### 4. What to Look For
Key error indicators:
- `BT disconnected` messages
- `err:` or `WRN:` prefixed lines
- Connection parameter mismatches
- Authentication failures
- Split communication errors

### 5. Save and Share Logs
1. Copy the entire log output
2. Look specifically for errors around the time of disconnection
3. Pay attention to:
   - Connection establishment messages
   - Security/pairing messages
   - Any error codes (especially negative numbers)

## Common Issues and Solutions

### "Connection rejected" or "Security failed"
- Indicates pairing data corruption → Run settings reset

### "Split connection failed"
- Check that both halves are powered
- Ensure left half is plugged in via USB (it's the central)

### "Out of memory" errors
- Too many features enabled for the board
- May need to disable some features

### "GATT" or "ATT" errors
- Bluetooth profile issues
- May need to clear pairings on both keyboard and computer

## Reverting Debug Mode
After debugging, disable logging to save power and improve performance:
1. Edit `config/totem.conf`
2. Change `CONFIG_ZMK_USB_LOGGING=y` to `CONFIG_ZMK_USB_LOGGING=n`
3. Remove or comment out the debug logging lines
4. Rebuild and flash normal firmware