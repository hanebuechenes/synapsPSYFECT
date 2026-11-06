# synapsPSYFECT

**synapsPSYFECT** is a high-end, 6-sheet multi-stage analog/hybrid FX Eurorack module designed for deep signal manipulation, multi-effect cross-modulation, and active spatial shaping.

The module combines a 4-Stage Vactrol Phaser, a Dual PT2399 Delay, and an LM13700-based Quadrature Frequency Shifter/Ring Modulator, all interconnected through a flexible active summing cross-modulation matrix.

---

## Technical Features & Architecture

* **Multi-Stage Architecture:** 6 dedicated schematic sheets covering Power, CV Buffering, Matrix Summing, Phaser, Dual Delay, and Frequency Shifter.
* **Active Input Buffering & Summing Matrix (`U12C`/`U4`/`U5`):** Dedicated TL074 operational amplifier buffers for all audio inputs and cross-modulation feedback paths to prevent crosstalk and signal bleed.
* **4-Stage Vactrol Phaser (`U7`/`U6`, `U8`, `U10`, `U11`):** All-pass filter architecture utilizing VTL5C vactrols for smooth, organic, analog phase shifting with CV control (`PHASER_CV`) and manual resonance feedback (`RES_POT1`).
* **Dual PT2399 Delay (`U12`/`U13`):** Two PT2399 ICs with voltage-controlled delay time (`DELAY_TIME_CV` via `Q2`/`Q3`) and transistor-shunt feedback modulation (`FEEDBACK_CV` via `Q4`).
* **LM13700 Frequency Shifter (`U14`/`U5`/`U9`):** Quadrature carrier oscillator generating sine/cosine phases (`CARRIER_SIN`/`CARRIER_COS`) driving a dual-OTA LM13700 for true frequency shifting and ring modulation (`SHIFT_CV`).
* **BOM & Component Standards:** SMD implementation (0603 / 0805 passives). **Strictly 0% Tantalum capacitors**, relying on NP0/C0G MLCCs for frequency-critical audio paths, X7R/X5R MLCCs, and SMD Aluminum Electrolytic capacitors for power rail filter banks.

---

## Module Specifications

| Specification | Parameter / Value |
| :--- | :--- |
| **Format** | Eurorack Synthesis Module |
| **Power Supply** | $\pm 12\text{VDC}$ Eurorack Standard Bus |
| **Internal Rails** | $+12\text{VA}$, $-12\text{VA}$, $+5\text{V}$, $+3.3\text{V}$, $+1.65\text{V\_REF}$ |
| **Input CV Protection** | $100\text{k}\Omega$ series resistors with 1N4148W clamping diodes & TL074 buffer stages |
| **Passive Component Sizes** | SMD 0603 (resistors & decoupling), SMD 0805 / 1206 (capacitors) |
| **IC Footprints** | SOIC-14, SOP-16, SOIC-16, SOT-223 |

---

## Signal Flow Overview

```
                          +------------------------+
                          |  CV Inputs (Protected) |
                          +-----------+------------+
                                      |
                                      v
  [AUDIO_IN] ---> [Input Buffer] ---> ( Matrix / Routing ) ---> [Phaser Stage (VTL5C)]
                       |                     |             ---> [Dual PT2399 Delay]
                       |                     |             ---> [LM13700 Freq Shifter]
                       v                     v
                 +-------------------------------+
                 | Active Cross-Mod Summing      | ---> [Audio Output]
                 | & Dry/Wet Mix (TL074)         |
                 +-------------------------------+
```

---

## Procurement & Assembly Notes

* **Capacitor Types:** 
  * Use **NP0/C0G** dielectrics for $10\text{nF}$ capacitors in the Phaser (`C13`–`C16`) and Quadrature Oscillator (`C35`–`C36`) to minimize temperature drift and microphonics.
  * Use **X7R/X5R** for all $100\text{nF}$ decoupling capacitors (`C39`–`C48` placed directly at TL074 power pins 4 & 11).
* **SMD Hand-Soldering:** 0603/0805 components chosen for manageable DIY manual assembly or automated SMT placement (JLCPCB compatible).

---

## Repository Structure

```
├── hardware/              # KiCad project files (.kicad_pro, .kicad_sch, .kicad_pcb)
├── bom/                   # Bill of Materials (BOM exports / iBOM)
├── docs/                  # Gerber files, schematic PDFs, and design notes
├── .gitignore             # KiCad temporary & build file exclusions
└── README.md              # Project documentation
```

---

## License

Hardware open-source project created by **hanebuechenes / synaps**. Distributed under the CERN-OHL-P (Permissive) or MIT License.