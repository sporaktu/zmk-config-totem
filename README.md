<picture>
  <source media="(prefers-color-scheme: dark)" srcset="/docs/images/TOTEM_logo_dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="/docs/images/TOTEM_logo_bright.svg">
  <img alt="TOTEM logo font" src="/docs/images/TOTEM_logo_bright.svg">
</picture>

# ZMK CONFIG FOR THE TOTEM SPLIT KEYBOARD

[Here](https://github.com/GEIGEIGEIST/totem) you can find the hardware files and build guide.\
[Here](https://github.com/GEIGEIGEIST/qmk-config-totem) you can find the QMK config for the TOTEM.

TOTEM is a 38 key column-staggered split keyboard running [ZMK](https://zmk.dev/) or [QMK](https://docs.qmk.fm/). It's meant to be used with a SEEED XIAO BLE or RP2040.


![TOTEM layout](/docs/images/TOTEM_layout.svg)



## HOW TO USE

### Option 1: GitHub Actions (Recommended for simple edits)
- fork this repo
- `git clone` your repo, to create a local copy on your PC (you can use the [command line](https://www.atlassian.com/git/tutorials) or [github desktop](https://desktop.github.com/))
- adjust the totem.keymap file (find all the keycodes on [the zmk docs pages](https://zmk.dev/docs/codes/))
- `git push` your repo to your fork
- on the GitHub page of your fork navigate to "Actions"
- scroll down and unzip the `firmware.zip` archive that contains the latest firmware
- connect the left half of the TOTEM to your PC, press reset twice
- the keyboard should now appear as a mass storage device
- drag'n'drop the `totem_left-seeeduino_xiao_ble-zmk.uf2` file from the archive onto the storage device
- repeat this process with the right half and the `totem_right-seeeduino_xiao_ble-zmk.uf2` file.

### Option 2: Local Build with Docker and Dev Container

#### Prerequisites
1. Install [Docker Desktop](https://www.docker.com/products/docker-desktop/)
2. Install the Dev Container CLI: `npm install -g @devcontainers/cli`
3. Clone the ZMK repository:
   ```bash
   git clone https://github.com/zmkfirmware/zmk.git
   ```

#### Setup

1. Create a volume for this config:
   ```bash
   docker volume create --driver local -o o=bind -o type=none -o device="/absolute/path/to/zmk-config-totem" zmk-config-totem
   ```
   For Windows PowerShell:
   ```powershell
   docker volume create --driver local -o o=bind -o type=none -o device="C:/Projects/keyboards/zmk-config-totem" zmk-config-totem
   ```

2. Navigate to the ZMK directory:
   ```bash
   cd /path/to/zmk
   ```

3. Start the dev container:
   ```bash
   devcontainer up --workspace-folder .
   ```

4. Connect to the container:
   ```bash
   docker ps  # Find the container ID
   docker exec -w /workspaces/zmk -it <container_id> /bin/bash
   ```

#### Building Firmware

Inside the container, initialize the workspace (first time only):
```bash
west init -l app/
west update
```

Build for left side:
```bash
west build -d build/left -b seeeduino_xiao_ble -s app -- -DZMK_CONFIG="/workspaces/zmk-config-totem/config" -DSHIELD=totem_left
```

Build for right side:
```bash
west build -d build/right -b seeeduino_xiao_ble -s app -- -DZMK_CONFIG="/workspaces/zmk-config-totem/config" -DSHIELD=totem_right
```

The firmware files will be in:
- Left: `build/left/zephyr/zmk.uf2`
- Right: `build/right/zephyr/zmk.uf2`

#### Alternative: Direct Docker Command

If you prefer not to use devcontainer CLI:

```bash
docker run -it --rm \
  -v /path/to/zmk-config-totem/config:/workspaces/zmk/config \
  -v zmk-root-user:/root \
  -v zmk-zephyr:/workspaces/zmk/zephyr \
  -v zmk-zephyr-modules:/workspaces/zmk/modules \
  -v zmk-zephyr-tools:/workspaces/zmk/tools \
  -w /workspaces/zmk \
  zmkfirmware/zmk-dev-arm:3.5 /bin/bash
```

For Windows PowerShell (single line):
```powershell
docker run -it --rm -v C:\Projects\keyboards\zmk-config-totem\config:/workspaces/zmk/config -v zmk-root-user:/root -v zmk-zephyr:/workspaces/zmk/zephyr -v zmk-zephyr-modules:/workspaces/zmk/modules -v zmk-zephyr-tools:/workspaces/zmk/tools -w /workspaces/zmk zmkfirmware/zmk-dev-arm:3.5 /bin/bash
```

## KEYMAP FEATURES

This configuration includes:
- QWERTY layout with homerow mods
- Hold X for system/adjust layer
- Optimized timing for homerow mods (250ms tap term)
- Layer tap on Tab (NAV), Escape (SYM), and X (ADJ)

### Base Layer (QWERTY)
```
             Q  W  E  R  T      Y  U  I  O  P
             A  S  D  F  G      H  J  K  L  ;
          Q  Z  X  C  V  B      N  M  ,  .  /  \
                   DEL TAB SPC  RET ESC BSPC
```

### Homerow Mods
- A: GUI (Win/Cmd)
- S: Alt
- D: Ctrl
- F: Shift
- J: Shift
- K: Ctrl
- L: Alt
- ;: GUI (Win/Cmd)

### Layer Keys
- Hold TAB: Navigation layer (NAV)
- Hold ESC: Symbol layer (SYM)
- Hold X: Adjust/System layer (ADJ)

### Combos
- Q+W: ESC
- A+S: Q
- L+;: P
- S+D+F: Toggle TVP layer

### Navigation Layer (NAV)
```
           ESC CLR ↑  =  [      ]  7  8  9  +
           SFT ←  ↓  →  [      ]  4  5  6  -
         Q DEL PGU CPS PGD (      )  1  2  3  *
                   ___ TAB SPC  ADJ 0  ___
```

### Symbol Layer (SYM)
```
           !  @  #  $  %      ^  &  Ü  '  "
           Ä  _  ß  _  _      MUTE ¥  €  £  Ö
         _ @1 @2  _  _  _      VOL- VOL+ PREV NEXT \ _
                   ___ GIF ADJ  ___ PLAY ___
```

### Adjust Layer (ADJ)
```
           RST CLR OUT _  _      _  F7 F8 F9 F12
           BOOT NXT _  _  _      _  F4 F5 F6 F11
         _ _  PRV _  _  _      _  F1 F2 F3 F10 _
                   ___ ___ ___  ___ ___ ___
```

### Bluetooth Controls (ADJ Layer)
- Hold X+W: Clear all Bluetooth profiles
- Hold X+Q: Connect to Bluetooth profile 0
- Hold X+E: Toggle between USB and Bluetooth output