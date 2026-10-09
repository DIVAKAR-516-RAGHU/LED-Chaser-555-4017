# 10-Stage Sequential LED Chaser (NE555 + CD4017)

A fully verified, 2-layer hardware design of a 10-stage sequential LED chaser circuit designed in **KiCad**. The board incorporates an analog astable pulse generator driving a CMOS Johnson decade counter with dedicated current-limited output stages and integrated ground copper fills.

---

## ⚡ Circuit Overview & Working Principle

The circuit is organized into three sequential functional stages:

1. **Clock Generator (NE555 Timer - Astable Mode):**
   * Configured as an astable multivibrator producing continuous square-wave clock pulses.
   * Timing is governed by external resistors $R_1$, $R_2$ and timing capacitor $C_1$:
     $$f \approx \frac{1.44}{(R_1 + 2R_2) \cdot C_1}$$
   * The output from pin 3 feeds directly into the clock input of the counter.

2. **Decade Counter & Sequencer (CD4017):**
   * High-speed CMOS 5-stage Johnson decade counter with 10 decoded active-high outputs ($Q_0$ through $Q_9$).
   * Advances one count on every positive clock edge received from the 555 timer.
   * Clock Inhibit (pin 13) and Master Reset (pin 15) are tied to ground for continuous, rollover cycling.

3. **Output Display (LED Array):**
   * 10 sequential 5 mm LEDs ($D_1$ to $D_{10}$), each paired with an independent 1 kΩ current-limiting resistor ($R_3$ to $R_{12}$) to maintain uniform brightness and prevent current crowding.

---

## 🛠️ Hardware & PCB Specifications

* **EDA Tool:** KiCad 8.0+
* **Layer Count:** 2-Layer (Top Copper / Bottom Copper)
* **Board Dimensions:** Defined via enclosed `Edge.Cuts` boundary
* **Substrate / Thickness:** FR-4 / 1.6 mm
* **Copper Weight:** 1 oz (35 µm)
* **Minimum Trace Width:** 0.25 mm (Signals) / 0.5 mm (Power rails)
* **Ground Strategy:** Solid ground fill on bottom copper (`B.Cu`) with thermal relief spokes on all grounded through-hole pads.
* **Decoupling / EMI Protection:** Dedicated 100 nF ceramic bypass capacitors located directly adjacent to $V_{CC}$ and $V_{DD}$ supply pins to suppress switching transients.
* **Design Verification:** Passed with **0 ERC (Electrical Rules Check)** and **0 DRC (Design Rules Check)** errors.

---

## 📋 Bill of Materials (BOM)

| Designator | Description / Value | Package / Footprint | Quantity |
| :--- | :--- | :--- | :--- |
| **U1** | NE555 Precision Timer IC | DIP-8 | 1 |
| **U2** | CD4017 Decade Counter/Divider IC | DIP-16 | 1 |
| **D1 – D10** | 5 mm Through-Hole LEDs | Radial LED 5 mm | 10 |
| **R1** | 10 kΩ Resistor, 1/4W | Axial Through-Hole | 1 |
| **R2** | 100 kΩ Resistor, 1/4W | Axial Through-Hole | 1 |
| **R3 – R12** | 1 kΩ Resistors, 1/4W | Axial Through-Hole | 10 |
| **C1** | 10 µF Electrolytic Capacitor | Radial 2.54 mm pitch | 1 |
| **C2** | 10 nF Ceramic Disc Capacitor | Radial 2.54 mm pitch | 1 |
| **C3, C4** | 100 nF Ceramic Bypass Capacitors | Radial 2.54 mm pitch | 2 |
| **J1** | 2-Pin Screw Terminal or 2.54 mm Header | 1x02 2.54 mm Pitch | 1 |

---

## 📁 Repository Structure

```text
├── Hardware/                         # Native KiCad design files
│   ├── LED Chaser (CD4017 + 555).kicad_pro
│   ├── LED Chaser (CD4017 + 555).kicad_sch
│   └── LED Chaser (CD4017 + 555).kicad_pcb
├── Production/                       # Manufacturing outputs
│   └── LED_Chaser_Fabrication.zip   # Gerber & Excellon drill files
├── assets/                           # Media & layout previews
│   ├── 3d_render.png
│   ├── pcb_layout.png
│   └── schematic_preview.png
├── .gitignore
└── README.md
