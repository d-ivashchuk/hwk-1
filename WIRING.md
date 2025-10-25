# Scotto9 Wiring Guide for nice!nano v2

## Overview

This is a 3x3 macropad with 9 keys arranged in a grid layout.

## Pin Assignments

### Your nice!nano Board Pin Labels

Your board shows GPIO numbers directly (like 022, 024, 100). These correspond to nRF52840 pins.

### Columns (connect to switch columns, right to left)

- **Column 0 (rightmost)**: Pin labeled **017** (P0.17)
- **Column 1 (middle)**: Pin labeled **020** (P0.20)
- **Column 2 (leftmost)**: Pin labeled **022** (P0.22)

### Rows (connect to switch rows, top to bottom)

- **Row 0 (top)**: Pin labeled **031** (P0.31)
- **Row 1 (middle)**: Pin labeled **029** (P0.29)
- **Row 2 (bottom)**: Pin labeled **002** (P0.02)

## Key Layout

```
┌───┬───┬───┐
│ 7 │ 8 │ 9 │  ← Row 0 (connect to pin 031)
├───┼───┼───┤
│ 4 │ 5 │ 6 │  ← Row 1 (connect to pin 029)
├───┼───┼───┤
│ 1 │ 2 │ 3 │  ← Row 2 (connect to pin 002)
└───┴───┴───┘
  ↑   ↑   ↑
Col2 Col1 Col0
022  020  017  ← Look for these numbers on your board!
```

## Two orientations (avoid mirroring mistakes)

The matrix doesn’t change, but your view does. Use the diagram that matches how you’re holding the board.

### Front view — keys UP (switches/keycaps facing you)

You’ll route columns vertically; rows leave to the MCU at the right edge.

```
               Columns (right → left)
            C0      C1      C2
           017     020     022
         ┌──────┬──────┬──────┐
Row 0 →  │  7   │  8   │  9   │  → MCU pin 031
         ├──────┼──────┼──────┤
Row 1 →  │  4   │  5   │  6   │  → MCU pin 029
         ├──────┼──────┼──────┤
Row 2 →  │  1   │  2   │  3   │  → MCU pin 002
         └──────┴──────┴──────┘
            ↑      ↑      ↑
           017    020    022 (MCU column pins)
```

### Back view — keys DOWN (you see the diodes)

Flip the board over and everything is mirrored left↔right. Columns appear left→right.

```
          Columns (left → right when viewed from the back)
            C2      C1      C0
           022     020     017
         ┌──────┬──────┬──────┐
MCU 031 ←│  7   │  8   │  9   │  ← Row 0
         ├──────┼──────┼──────┤
MCU 029 ←│  4   │  5   │  6   │  ← Row 1
         ├──────┼──────┼──────┤
MCU 002 ←│  1   │  2   │  3   │  ← Row 2
         └──────┴──────┴──────┘
            022    020    017
            C2     C1     C0  (MCU column pins)
```

## Finding Pins on Your nice!nano Board

Look for these pin labels on your board:

**For COLUMNS (switches):**

- Find **017** → Column 0 (rightmost keys: 9, 6, 3)
- Find **020** → Column 1 (middle keys: 8, 5, 2)
- Find **022** → Column 2 (leftmost keys: 7, 4, 1)

**For ROWS (diodes):**

- Find **031** → Row 0 (top keys: 7, 8, 9)
- Find **029** → Row 1 (middle keys: 4, 5, 6)
- Find **002** → Row 2 (bottom keys: 1, 2, 3)

## Wiring Instructions

### Matrix Wiring (COL2ROW)

1. **Diode Direction**: Cathode (black band) towards the ROWS
2. Each switch has a diode connected to one leg
3. The diode cathodes on each row are connected together
4. The other leg of each switch on each column is connected together

Diode orientation visual

```
Switch leg ──►|── Row wire
                     ^
                     black band (cathode) → faces the ROW bus

Column wire ── Switch other leg
```

Why this matters

- With COL2ROW, the firmware drives COLUMNS and reads ROWS. Putting the diode’s
  band toward the ROW ensures current flows from a driven column into the row
  only when a key is pressed, preventing ghosting.

### Step-by-Step:

1. Place your 9 switches in the 3x3 grid
2. Solder a 1N4148 diode to each switch (cathode side)
3. **Row wiring**:
   - Connect all diode cathodes in Row 0 together → pin **031**
   - Connect all diode cathodes in Row 1 together → pin **029**
   - Connect all diode cathodes in Row 2 together → pin **002**
4. **Column wiring**:
   - Connect all switch pins in Column 0 (right) together → pin **017**
   - Connect all switch pins in Column 1 (middle) together → pin **020**
   - Connect all switch pins in Column 2 (left) together → pin **022**

## Key Functions (as programmed)

- Key 7: Cmd+Opt+7
- Key 8: Cmd+Opt+8
- Key 9: Cmd+Opt+9
- Key 4: Cmd+Opt+4
- Key 5: Cmd+Opt+5
- Key 6: Cmd+Opt+6
- Key 1: Cmd+Opt+1
- Key 2: Cmd+Opt+2
- Key 3: Cmd+Opt+3

## nice!nano Board Pin Reference

Your board uses direct GPIO numbering. Here's what you need:

### Pins You'll Use:

| **Pin Label on Board** | Full GPIO Name | What to Connect          |
| ---------------------- | -------------- | ------------------------ |
| **017**                | P0.17          | Column 0 (right column)  |
| **020**                | P0.20          | Column 1 (middle column) |
| **022**                | P0.22          | Column 2 (left column)   |
| **029**                | P0.29          | Row 1 (middle row)       |
| **031**                | P0.31          | Row 0 (top row)          |
| **002**                | P0.02          | Row 2 (bottom row)       |

**Note:** All pins are P0.XX (gpio0) - nice and symmetrical!

## Flashing

Once wired, double-tap the reset button on the nice!nano and drag the `scotto9-nice_nano_v2.uf2` file onto the NICENANO drive.
