# Scotto9 Macropad - Setup Complete

## What's Been Configured

Your ZMK firmware is now configured for a Scotto9 macropad (3x3 = 9 keys) using a nice!nano v2 controller.

### Files Created

1. **Shield Definition** (`config/boards/shields/scotto9/`)

   - `scotto9.dtsi` - Hardware pin definitions
   - `scotto9.overlay` - Shield overlay file
   - `Kconfig.shield` - Shield configuration
   - `Kconfig.defconfig` - Default config
   - `scotto9.conf` - Wired-only settings (Bluetooth disabled)

2. **Keymap** (`config/scotto9.keymap`)

   - Each key sends Cmd+Option+Number (1-9)
   - Layout matches number pad layout

3. **Build Configuration** (`.github/workflows/build.yml`)

   - Configured to build for nice!nano v2
   - Will create `scotto9-nice_nano_v2.uf2` file

4. **Wiring Guide** (`WIRING.md`)
   - Complete pin assignments
   - Wiring instructions
   - Visual layout diagram

## Pin Assignments for Wiring

## 📌 Pin Wiring Reference

When you build your keyboard, connect these pins (look for these numbers on your board):

| Pin Label | GPIO | Connect To | Keys |
|-----------|------|------------|------|
| **017** | P0.17 | Column 0 (right) | 9, 6, 3 |
| **020** | P0.20 | Column 1 (middle) | 8, 5, 2 |
| **022** | P0.22 | Column 2 (left) | 7, 4, 1 |
| **031** | P0.31 | Row 0 (top) | 7, 8, 9 |
| **029** | P0.29 | Row 1 (middle) | 4, 5, 6 |
| **002** | P0.02 | Row 2 (bottom) | 1, 2, 3 |

## Next Steps

1. **Build the firmware:**

   - Push these changes to GitHub
   - GitHub Actions will automatically build the firmware
   - Download `scotto9-nice_nano_v2.uf2` from the Actions artifacts

2. **Wire your keyboard:**

   - Follow the `WIRING.md` guide
   - Use 9 MX switches and 9 1N4148 diodes
   - Diode cathode (black band) goes toward the ROW wire

3. **Flash the firmware:**

   - Double-tap reset button on nice!nano v2
   - NICENANO drive will appear
   - Drag and drop the `.uf2` file
   - Board will automatically reboot

4. **Test:**
   - Plug in via USB
   - Press each key to verify Cmd+Opt+Number shortcuts work
   - Adjust keymap as needed in `config/scotto9.keymap`

## Modifying the Keymap

Edit `config/scotto9.keymap` to change what each key does. Current layout:

```
┌─────────┬─────────┬─────────┐
│ Cmd+Opt │ Cmd+Opt │ Cmd+Opt │
│   +7    │   +8    │   +9    │
├─────────┼─────────┼─────────┤
│ Cmd+Opt │ Cmd+Opt │ Cmd+Opt │
│   +4    │   +5    │   +6    │
├─────────┼─────────┼─────────┤
│ Cmd+Opt │ Cmd+Opt │ Cmd+Opt │
│   +1    │   +2    │   +3    │
└─────────┴─────────┴─────────┘
```

Replace `&kp LG(LA(N7))` with any key code you want. Examples:

- `&kp A` - Letter A
- `&kp C_MUTE` - Mute
- `&kp C_VOL_UP` - Volume up
- `&kp LG(LA(N1))` - Cmd+Opt+1

Push changes to GitHub to rebuild the firmware.
