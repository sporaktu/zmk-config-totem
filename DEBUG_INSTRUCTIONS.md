# Bluetooth Debug Instructions for Totem Keyboard

## How to Capture Debug Logs

### 1. Build and Flash Debug Firmware
- Commit and push the changes to trigger GitHub Actions build
- Download and flash the new firmware with debug logging enabled

### 2. Connect via RTT (Real-Time Transfer) for Debug Logs

**Note:** The Seeeduino XIAO BLE uses RTT logging instead of USB serial logging.

#### Using J-Link RTT Viewer (Recommended)
1. Install [J-Link Software](https://www.segger.com/downloads/jlink/)
2. Connect a J-Link debugger to the SWD pins on the XIAO BLE
3. Open J-Link RTT Viewer
4. Connect to the target device
5. Logs will appear in real-time

#### Alternative: OpenOCD with RTT
1. Install OpenOCD with RTT support
2. Create config file for nRF52840:
```
source [find interface/jlink.cfg]
transport select swd
source [find target/nrf52.cfg]
rtt setup 0x20000000 0x10000 "SEGGER RTT"
rtt start
rtt server start 9090 0
```
3. Connect: `telnet localhost 9090`

#### Simplest Option: Disable Bluetooth and Use USB Serial
If you don't have a debugger, temporarily test with USB only:
1. Comment out Bluetooth configs
2. Use USB connection to test other features

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
2. Comment out or remove all the RTT and LOG config lines:
   - `CONFIG_USE_SEGGER_RTT=y`
   - `CONFIG_RTT_CONSOLE=y`
   - `CONFIG_LOG=y`
   - `CONFIG_LOG_BACKEND_RTT=y`
   - etc.
3. Rebuild and flash normal firmware