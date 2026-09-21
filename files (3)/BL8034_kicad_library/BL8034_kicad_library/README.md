# BL8034 KiCad Library (Symbol + Footprint)

Based on Shanghai Belling **BL8034** datasheet V1.3 (4A, 16V Synchronous Step-Down Converter, ESOP8).

## Files
- `BL8034.kicad_sym` — schematic symbol (9 pins: 8 signal pins + thermal pad as pin 9)
- `BL8034.pretty/ESOP8_5.0x6.0mm_P1.27mm_EP2.4x3.3mm.kicad_mod` — PCB footprint

## Pinout (from datasheet)
| Pin | Name | Function |
|---|---|---|
| 1 | BST | High-side gate drive boost input |
| 2 | VIN | Power input |
| 3 | SW  | Switching node (to inductor) |
| 4 | GND | Ground |
| 5 | FB  | Feedback (Vref = 0.923V) |
| 6 | NC  | No connect |
| 7 | EN  | Enable (active high) |
| 8 | NC  | No connect |
| 9 | PAD | Exposed thermal pad — internally GND, must be soldered to PCB GND plane |

## Footprint dimensions (from datasheet Package Outline, mm, nominal)
- Body: D 4.90 x E1 3.90
- Overall lead span E: 6.00
- Pitch e: 1.27 (4 pins per side)
- Lead pad: 1.55 x 0.60 (generous solder pad, IPC-style, centered at ±2.7075mm)
- Exposed pad (pin 9): D1 x E2 = 3.30 x 2.40, with a 5-via thermal relief pattern (0.3mm drill / 0.6mm pad) tied to the pad for heat spreading to inner/bottom copper, per the datasheet's PCB layout recommendation ("GND plane area...should be maximized," "multiple via connections").

This matches the standard JEDEC MS-012 SOIC-8 body/lead footprint with an added exposed pad — equivalent in size to common "SOIC-8-1EP_3.9x4.9mm_P1.27mm" style footprints, but pad sizes here are calculated directly from the BL8034 datasheet's dimension table rather than a generic library part.

## How to use in KiCad (6.x / 7.x / 8.x)

### Option A — Project-local library (recommended for a single project)
1. Copy the whole `BL8034_kicad` folder (or just `BL8034.kicad_sym` and `BL8034.pretty/`) into your project directory.
2. In KiCad's **Symbol Editor** / **Schematic Editor**: `Preferences → Manage Symbol Libraries → Project Specific Libraries`, add a new row pointing to `BL8034.kicad_sym`, nickname e.g. `BL8034`.
3. In **PCB Editor**: `Preferences → Manage Footprint Libraries → Project Specific Libraries`, add a new row pointing to the `BL8034.pretty` folder, nickname e.g. `BL8034`.
4. Place the symbol from the `BL8034` library in your schematic — the `Footprint` field is already pre-linked to `BL8034:ESOP8_5.0x6.0mm_P1.27mm_EP2.4x3.3mm`.

### Option B — Global library (available in all projects)
Same as above but use `Global Libraries` instead of `Project Specific Libraries` in each Manage Libraries dialog, and store the files somewhere permanent (e.g. `Documents/KiCad/libraries/BL8034/`).

## Notes / things worth double-checking before fabrication
- Lead pad size (1.55 x 0.60mm) is a standard soldering-friendly SOIC-8 pad, slightly larger than the bare lead footprint (b=0.42, L≈0.6mm typ) for reliable reflow — adjust if your fab/assembly house has different pad guidelines.
- The exposed pad's thermal-via pattern is a common default (5x 0.3mm drill vias); tune via count/size to your stack-up and current fusing/thermal requirements.
- Always verify pad geometry against the datasheet's package outline drawing (page 5) and your PCB house's DFM rules before ordering boards, especially for a 4A part where thermal pad soldering quality matters.
