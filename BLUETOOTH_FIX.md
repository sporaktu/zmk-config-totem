# Totem Keyboard Bluetooth Fix Guide

## Problem
Bluetooth disconnects immediately after pairing with the Totem split keyboard using Seeeduino XIAO BLE.

## Solution
The issue is typically caused by corrupted Bluetooth pairing data in the keyboard's flash memory. A settings reset resolves this.

## Steps to Fix

1. **Build Settings Reset Firmware**
   - The `build.yaml` already includes the settings_reset configuration
   - GitHub Actions will automatically build three firmware files:
     - `totem_left-seeeduino_xiao_ble-zmk.uf2`
     - `totem_right-seeeduino_xiao_ble-zmk.uf2`
     - `settings_reset-seeeduino_xiao_ble-zmk.uf2`

2. **Flash Settings Reset**
   - Download the `settings_reset-seeeduino_xiao_ble-zmk.uf2` from GitHub Actions artifacts
   - Flash to **both halves** of the keyboard:
     1. Double-tap reset button to enter bootloader mode (drive appears)
     2. Copy settings_reset firmware to the drive
     3. Keyboard will reset automatically
     4. Repeat for the other half

3. **Flash Normal Firmware**
   - After settings reset, flash the regular firmware:
     1. Flash `totem_left-seeeduino_xiao_ble-zmk.uf2` to left half
     2. Flash `totem_right-seeeduino_xiao_ble-zmk.uf2` to right half

4. **Pair with Computer**
   - Remove any existing Totem keyboard entries from your computer's Bluetooth devices
   - Put keyboard in pairing mode (if needed)
   - Pair fresh with your computer

## Prevention
- Always unpair from computer's Bluetooth settings before reflashing firmware
- Use settings reset if switching between computers or after firmware experiments

## Configuration Notes
The following settings in `totem.conf` are critical for proper Bluetooth operation:
- `CONFIG_NFCT_PINS_AS_GPIOS=y` - Required because Totem uses D4/D5 pins (NFC antenna pins)
- `CONFIG_ZMK_SPLIT_ROLE_CENTRAL=y` - Ensures stable split keyboard connection
- Connection interval settings for stability

## References
- [ZMK Reset Documentation](https://zmk.dev/docs/troubleshooting#reset-settings)
- [Original Totem Config](https://github.com/GEIGEIGEIST/zmk-config-totem)