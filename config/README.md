# YellowJacket Keyboard Configuration

A comprehensive ZMK configuration for the YellowJacket split ergonomic keyboard supporting both **QWERTY** and **Colemak** layouts with 8 specialized layers and extensive combo functionality.

> 💡 The keyboard design is based on the [Yellow Jacket keyboard by jimmerricks](https://github.com/jimmerricks/bugs), with custom modifications tailored for the Yellow Jacket layout.

## Table of Contents
- [Layout Selection](#layout-selection)
- [Physical Layout](#physical-layout)
- [Base Layers](#base-layers)
- [Home Row Mods](#home-row-mods)
- [Layers](#layers)
- [Combos](#combos)
- [Usage Guide](#usage-guide)
- [Tips and Tricks](#tips-and-tricks)
- [Getting Started](#getting-started)

## Layout Selection

This configuration supports both QWERTY and Colemak base layouts. Choose your preferred layout by copying the appropriate keymap file:

### Available Layouts:
- **QWERTY**: `yellowjacket-qwerty.keymap` - Standard QWERTY layout
- **Colemak**: `yellowjacket-colemak.keymap` - Colemak layout for efficiency

### Switching Layouts:

**For QWERTY (current default):**
```bash
cp config/yellowjacket-qwerty.keymap config/yellowjacket.keymap
```

**For Colemak:**
```bash
cp config/yellowjacket-colemak.keymap config/yellowjacket.keymap
```

After copying, build your firmware as usual. The active layout is determined by the `yellowjacket.keymap` file used in the build process.

## Physical Layout

```
Key Position Reference:
╭────────────────────╮ ╭────────────────────╮
│      0   1   2   3 │ │  4   5   6   7     │
│  8   9  10  11  12 │ │ 13  14  15  16  17 │
│ 18  19  20  21  22 │ │ 23  24  25  26  27 │
╰───────────╮ 28  29 │ │ 30  31 ╭───────────╯
            ╰────────╯ ╰────────╯
```

## Base Layers

### QWERTY Layout

```
       Q     W     E     R         T     Y     U     I
GUI/A  ALT/S CTRL/D SHIFT/F G     H     SHIFT/J CTRL/K ALT/L GUI/;
FN/Z   SYS/X  C     V     B       N     M     ,     .     /
             NUM/SPACE BR/TAB   MOUS/BSPC ARR/ENTER
```

### Colemak Layout

```
       W     F     P     B         J     L     U     Y
GUI/A  ALT/R CTRL/S SHIFT/T G     M     SHIFT/N CTRL/E ALT/I GUI/O
FN/Z   SYS/X  C     D     V       K     H     ,     .     /
             NUM/SPACE BR/TAB   MOUS/BSPC ARR/ENTER
```

### Key Features:
- **Dual layout support** - Choose between QWERTY familiarity or Colemak efficiency
- **Home row modifiers** for efficient modifier access
- **Layer-tap keys** on thumbs and outer columns  
- **34-key layout** optimized for split ergonomic typing
- **Identical functionality** across both layouts (layers, combos, etc.)

## Home Row Mods

The home row keys double as modifiers when held:

### QWERTY Home Row Mods:
| Key | Tap | Hold |
|-----|-----|------|
| A | A | GUI (Windows/Cmd) |
| S | S | Alt |
| D | D | Ctrl |
| F | F | Shift |
| J | J | Shift |
| K | K | Ctrl |
| L | L | Alt |
| ; | ; | GUI (Windows/Cmd) |

### Colemak Home Row Mods:
| Key | Tap | Hold |
|-----|-----|------|
| A | A | GUI (Windows/Cmd) |
| R | R | Alt |
| S | S | Ctrl |
| T | T | Shift |
| N | N | Shift |
| E | E | Ctrl |
| I | I | Alt |
| O | O | GUI (Windows/Cmd) |

**Timing**: 150ms tapping term with tap-preferred behavior.

## Layers

### 1. NUM Layer (Number Pad)
**Activation**: Hold `Space` key

```
             -     -     -     -         -     7     8     9
       -     -     -     -     -         -     4     5     6     0
       -     -     -     -     -         -     1     2     3     .
                         ■     -         -     -
```

### 2. ARR Layer (Arrows & Navigation)
**Activation**: Hold `Enter` key  
**Toggle**: Combo `Space+Enter` (thumb keys)

```
             -     -     -     -       Scrl↑  Home   ↑    PgUp
       -     -     -     -     -       Scrl↓   ←     ↓     →    GUI
       -     -     -     -     -        Ins   End   Del   PgDn  TogARR
                         -     -         -     ■
```

### 3. MOUS Layer (Mouse Control)
**Activation**: Hold `Backspace` key  
**Toggle**: Combo `Backspace+;` (positions 17+30)

```
            MB2   MB3   MB1  Scrl↑     Scrl↑  MB1   M↑    MB2
      -     -     -     -    Scrl↓     Scrl↓  M←    M↓    M→    -
      -     -     -     -     -        MB4   ScrlL  MB3  ScrlR  MB5
                        -     -         ■     -
```

### 4. FUNC Layer (Function Keys)
**Activation**: Hold `Z` key

```
             F9    F10   F11   F12       -     -     -     -
      ■      F5    F6    F7    F8        -     -     -     -     -
      -      F1    F2    F3    F4        -     -     -     -     -
                         -     -         -     -
```

### 5. SYS Layer (System Controls)
**Activation**: Hold `X` key

```
             -     -     -    Vol+      OUT   -     -    Studio
      -      -     -    Play  Vol-      -     BT3   BT4   BT5   BT_CLR
      -      ■     -     -    Mute      -     BT0   BT1   BT2   BT_CLR_ALL
                         -     -         -     -
```

### 6. BR Layer (Brackets)
**Activation**: Hold `Tab` key

```
             -     {     }     -         -     -     -     -
      -      -     (     )     -         -     -     -     -     -
      -      -     [     ]     -         -     -     -     -     -
                         -     ■         -     -
```

### 7. GA Layer (Gaming)
**Activation**: Toggle with combo `R+I` (positions 4+7)

```
             Q     W     E     1         -     -     -     -
    Shift    A     S     D     2         -     -     -     -     -
    Ctrl     -     -     -     3         -     -     -     -     -
                       Space  Tab        -     -
```

### 8. Reserved Layers
Three additional layers (extra1, extra2, extra3) are reserved for future customization.

## Combos

Combos allow you to access additional characters and functions by pressing two keys simultaneously.

### Letters & Punctuation

| Combo | Keys (QWERTY) | Keys (Colemak) | Output | Description |
|-------|---------------|----------------|--------|-------------|
| P | S+D | R+S | P | P letter combo |
| Q | - | R+S | Q | Q letter combo (Colemak only) |
| : | K+L | E+I | : | Colon |
| ; | M+, | H+, | ; | Semicolon |
| Esc | D+F OR J+K | S+T OR N+E | Esc | Escape key |

### Quick Numbers
**Hold `Enter` + Right Hand Key**:

| Number | QWERTY Combo | Colemak Combo | Position |
|--------|--------------|---------------|----------|
| 0 | Enter+; | Enter+O | 31+17 |
| 1 | Enter+M | Enter+M | 31+24 |
| 2 | Enter+, | Enter+, | 31+25 |
| 3 | Enter+. | Enter+. | 31+26 |
| 4 | Enter+J | Enter+N | 31+14 |
| 5 | Enter+K | Enter+E | 31+15 |
| 6 | Enter+L | Enter+I | 31+16 |
| 7 | Enter+Y | Enter+L | 31+5 |
| 8 | Enter+U | Enter+U | 31+6 |
| 9 | Enter+I | Enter+Y | 31+7 |

### Special Characters
**Hold `Backspace` + Right Hand Key**:

| Character | QWERTY Combo | Colemak Combo | Position |
|-----------|--------------|---------------|----------|
| ! | Bspc+M | Bspc+M | 30+24 |
| @ | Bspc+, | Bspc+, | 30+25 |
| # | Bspc+. | Bspc+. | 30+26 |
| $ | Bspc+J | Bspc+N | 30+14 |
| % | Bspc+K | Bspc+E | 30+15 |
| ^ | Bspc+L | Bspc+I | 30+16 |
| & | Bspc+Y | Bspc+L | 30+5 |
| * | Bspc+U | Bspc+U | 30+6 |
| ( | Bspc+I | Bspc+Y | 30+7 |

### Quotes
**Hold `Space` + Left Hand Key**:

| Character | QWERTY Combo | Colemak Combo | Position |
|-----------|--------------|---------------|----------|
| ~ | Space+Z | Space+Z | 28+18 |
| ` | Space+S | Space+R | 28+9 |
| ' | Space+D | Space+S | 28+10 |
| " | Space+F | Space+T | 28+11 |

### Operators & Symbols

| Symbol | QWERTY Combo | Colemak Combo | Position | Description |
|--------|--------------|---------------|----------|-------------|
| = | N+Bspc | M+Bspc | 23+30 | Equals |
| + | T+Bspc | J+Bspc | 4+30 | Plus |
| - | H+Bspc | M+Bspc | 13+30 | Minus |
| _ | X+C | X+C | 19+20 | Underscore |
| \ | Bspc+/ | Bspc+/ | 30+27 | Backslash |
| \| | /+Enter | /+Enter | 27+31 | Pipe |

### Layer Toggles

| Function | QWERTY Combo | Colemak Combo | Position |
|----------|--------------|---------------|----------|
| Mouse Toggle | ;+Bspc | O+Bspc | 17+30 |
| Arrow Toggle | Bspc+Enter | Bspc+Enter | 30+31 |
| Gaming Toggle | R+I | B+Y | 4+7 |

### Special Functions

| Combo | Keys | Function |
|-------|------|----------|
| Turbo Shift | Both thumb keys | Shift (emergency shift) |

## Usage Guide

### Basic Typing
1. **Normal typing**: Use like any QWERTY keyboard
2. **Modifiers**: Hold home row keys for Ctrl, Alt, Shift, GUI
3. **Numbers**: Hold Space + right hand for number pad
4. **Arrows**: Hold Enter for navigation

### Layer Access Patterns
- **Temporary**: Hold layer key → type → release
- **Toggle**: Use combo to lock layer → type → toggle again to unlock
- **One-shot**: Tap layer key for single character access (where supported)

### Efficient Workflows

#### Programming
1. **Brackets**: Hold Tab for (), [], {}
2. **Numbers**: Hold Space for number pad
3. **Special chars**: Use Backspace combos for !@#$%^&*
4. **Navigation**: Hold Enter for arrows and page keys

#### Gaming
1. **Toggle gaming layer**: R+I combo
2. **Standard WASD** with left shift and ctrl
3. **Quick numbers** 1-3 on right side
4. **Toggle back**: R+I combo again

#### System Control
1. **Bluetooth**: Hold X → BT0-5 for pairing, BT_CLR to disconnect
2. **Media**: Hold X → Play/Pause, Volume controls
3. **Mouse**: Hold Backspace or toggle with ;+Backspace combo

## Tips and Tricks

### Home Row Mods
- **Practice slowly** - let muscle memory develop for the 150ms timing
- **Tap quickly** for letters, **hold deliberately** for modifiers
- **Use opposite hand** for modifier+key combinations when possible

### Combo Mastery
- **Thumb combos** are easiest - start with Space+letter for quotes
- **Practice number combos** with Enter+right hand keys
- **Emergency shift** (both thumbs) when home row mods fail

### Layer Efficiency
- **Learn one layer at a time** - start with NUM layer
- **Use toggles** for extended work in arrow/mouse layers
- **Gaming layer** completely changes left side - practice mode switching

### Troubleshooting
- **Stuck in layer?** Use the same toggle combo to exit
- **Modifier stuck?** Tap the home row key to release
- **Bluetooth issues?** Use BT_CLR_ALL in SYS layer

### Customization
- Modify `yellowjacket.keymap` for personal preferences
- Adjust `tapping-term-ms` in behaviors section for home row mod timing
- Add custom combos using the COMBO macro pattern

---

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/68mschmitt/yellowjacket-config.git
cd yellowjacket-config
```

### 2. Set Up the Environment

Follow the [ZMK development setup guide](https://zmk.dev/docs/development/setup) to install prerequisites and prepare your build environment.

### 3. Build the Firmware

Use `west` or your preferred build tool to compile the firmware. You can also reference `build.yaml` for common configurations.

### 4. Flash to Your Keyboard

Once built, flash the `.uf2` or `.hex` files to your Yellow Jacket keyboard using the appropriate method for your microcontroller (e.g., drag-and-drop UF2 flashing or DFU).

---

## Repository Structure

- `boards/shields/` - Custom shield definitions for the Yellow Jacket keyboard
- `config/` - Contains keymap configuration, layer definitions, and user preferences  
- `zephyr/` - Includes Zephyr RTOS configuration files used by ZMK
- `.github/workflows/` - GitHub Actions CI workflows for building and testing firmware
- `build.yaml` - Configuration file used for building the firmware with ZMK's west build system

---

## Contributing

Issues and pull requests are welcome. Feel free to suggest layout tweaks, firmware enhancements, or documentation improvements.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

---

*For technical details, see the `yellowjacket.keymap` configuration file.*

