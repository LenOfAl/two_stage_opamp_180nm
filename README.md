# Two-Stage Miller-Compensated Op-Amp — TSMC 180nm

A two-stage CMOS operational amplifier designed in Cadence Virtuoso using the
**gm/Id methodology** for transistor sizing, with a **common-centroid** layout
and full pre- vs post-parasitic-extraction (PEX) comparison.

Course project for **EE517 Analog VLSI Lab**, Department of EEE, IIT Guwahati.

## Design targets

| Specification | Target |
|---|---|
| Supply voltage (V<sub>DD</sub>) | 1.8 V |
| Load capacitance (C<sub>L</sub>) | 1 pF |
| DC gain | ≥ 50 dB |
| Gain-bandwidth product | ≥ 150 MHz |
| Phase margin | ≥ 60° |
| Slew rate | ≥ 5 V/µs |
| Common-mode gain | ≤ −10 dB |
| Output swing (differential p-p) | ≥ 800 mV<sub>pp</sub> |
| Power consumption | ≤ 1 mW |

## Results — pre- vs post-layout

Parasitic extraction was run on the common-centroid layout and the extracted
netlist re-simulated against the schematic-level results.

| Parameter | Pre-layout | Post-layout (PEX) | Change |
|---|---|---|---|
| DC gain | 60.63 dB | 58.52 dB | slight decrease |
| Unity-gain frequency | 167 MHz | 146 MHz | reduced |
| Phase margin | 56.61° | 58.60° | slightly increased |
| Slew rate | 176.6 V/µs | 149.0 V/µs | reduced |
| Common-mode gain | −11.17 dB | −22.07 dB | improved |
| CMRR | 67.79 dB | 80.68 dB | improved |

Interconnect and junction parasitics load the internal nodes, so gain, bandwidth
and slew rate all drop as expected. Phase margin improves slightly — the added
output-node capacitance pushes the non-dominant pole interaction in a favourable
direction — and common-mode rejection improves because the common-centroid
placement cancels the systematic gradient mismatch that dominates CMRR.

## Method

**gm/Id sizing** — transistors are sized from the gm/Id vs I<sub>D</sub>/(W/L)
characteristic rather than by hand-tuned square-law equations. The gm/Id ratio
directly sets the inversion region: high gm/Id gives more gain per unit current
(weak inversion, slower), low gm/Id gives more speed at higher current cost.
This makes the gain/bandwidth/power trade-off an explicit design knob and is
accurate across short-channel regions where square-law models break down.

**Common-centroid layout** — matched devices (the input differential pair and
current-mirror loads) are split into segments and interdigitated about a shared
centroid, so linear process gradients across the die cancel to first order.
This directly targets the offset and CMRR degradation that random and systematic
mismatch would otherwise cause.

## Repository contents

- [`2_stage_opamp_report.pdf`](2_stage_opamp_report.pdf) — full project report:
  theory, design procedure, schematics, layout, and pre/post-PEX simulation results.

## Authors

Group project, EE517 Analog VLSI Lab, IIT Guwahati:

- Yuvraj Singh
- Aritra Sarkar
- Ameya S Moghe
- Allen Joseph Jose

## Tools

Cadence Virtuoso (Schematic / Layout / ADE), Spectre, Calibre (DRC / LVS / PEX),
TSMC 180 nm CMOS process.
