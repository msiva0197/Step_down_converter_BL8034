# BL8034 Step-Down (Buck) Converter: 15V to 5V @ 2A

![Board Dimensions](https://img.shields.io/badge/Size-38mm_x_29mm-blue)
![Layers](https://img.shields.io/badge/Layers-2_Layer_PCB-green)
![Status](https://img.shields.io/badge/Status-Ready_for_Manufacturing-success)

## Overview

This repository contains an open-source, compact 2-layer PCB design for a DC-DC step-down converter using the **BL8034** synchronous buck regulator. This specific design is optimized to step down a **15V input to a stable 5V output**, supporting a continuous load current of **2A**. 

The design addresses critical power routing and thermal management requirements, ensuring stable operation without overheating or saturating the components.


## Key Specifications

* **Input Voltage (Vin):** 15V Nominal 
* **Output Voltage (Vout):** 5V
* **Continuous Output Current:** 2A
* **Switching Frequency:** High frequency (internal)
* **PCB Layers:** 2 Layers (Top/Bottom)
* **Dimensions:** 38 mm x 29 mm

## PCB Layout Highlights

To ensure safe and reliable 2A continuous operation, this layout incorporates several best practices:

* **1mm Power Polygons:** The critical high-current paths (`V_IN+`, `SW` node, and `V_OUT_5V`) utilize wide 1mm copper polygons instead of thin traces. This minimizes impedance, voltage drop, and localized heating.
* **Optimized Ground Loop:** The ground pad of the input capacitor (C1) is routed directly to the IC's exposed thermal pad (Pin 9) via a solid top-layer copper pour, drastically reducing high-frequency EMI.
* **Proper Component Sizing:** Avoiding standard 0603 packages for high-power paths. The inductor uses an NR5040 footprint to handle high saturation currents, and the main capacitors use 1206 packages to mitigate DC-bias capacitance loss at 15V.
* **Thermal Management:** Extensive thermal vias are placed under the BL8034 IC's exposed center pad to dissipate heat effectively into the bottom ground plane.

## Bill of Materials (BOM)

| Reference | Qty | Value | Footprint | Part Type / Description |
| :--- | :--- | :--- | :--- | :--- |
| **U1** | 1 | BL8034 | ESOP-8 | Synchronous Step-Down Converter IC |
| **L2** | 1 | 4.7µH | NR5040 | SMD Power Inductor (NR5040T4R7N, Isat > 3A) |
| **C1, C3** | 2 | 22µF | 1206 | Ceramic Capacitor (Minimum 25V rating for C1) |
| **C2** | 1 | 1µF | 0603 | Ceramic Boot Capacitor |
| **R2** | 1 | 2.2KΩ | 0603 | SMD Resistor (Feedback bottom) |
| **R3** | 1 | 10KΩ | 0603 | SMD Resistor (Feedback top) |
| **R4** | 1 | 100KΩ | 0603 | SMD Resistor (Enable Pull-up) |
| **TP1 - TP4**| 4 | - | 5.0x8.0mm | Terminal Pads for VIN+, VIN-, VOUT+, VOUT- |

*Note: Output voltage is set by the feedback resistor divider R3 and R2. $V_{OUT} = 0.923V \times (1 + 10k/2.2k) =5.118 volt$*

## Manufacturing Details

* **Gerber Files:** Available in the `releases` section or the `gerber/` folder.
* **Silkscreen Note:** The board features clear terminal labels (`V_IN+`, `V_IN-`, `V_OUT+`, `V_OUT-`) and mounting holes for easy enclosure integration.

## Disclaimer

This is an open-source hardware project provided "as-is". Please verify all component ratings (especially capacitor voltage ratings and inductor saturation currents) before assembly.
