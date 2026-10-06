# Low-Power 45 nm CMOS LNA for 2.4 GHz BLE Receivers (PCSNIM)

Undergraduate thesis, Universitas Gadjah Mada. Own design, from schematic to post-layout extraction.

## Overview

A low-noise amplifier for the front end of a 2.4 GHz Bluetooth Low Energy receiver, using the PCSNIM technique (power-constrained simultaneous noise and input matching) with inductive source degeneration and a cascode stage. Target specifications were derived from the Bluetooth Core Specification 6.0 [3].

Topology progression studied in the thesis: common-source, inductively degenerated common-source, SNIM, then PCSNIM [1], [2].

## Tools and flow

- Schematic and layout: Cadence Virtuoso
- Simulation: Spectre
- DRC / LVS: Pegasus
- Parasitic extraction: Quantus (post-layout results below)
- PDK: gpdk045

## Final design point

| Parameter | Value |
|---|---|
| Supply voltage Vdd | 1 V |
| Bias voltage Vgs (M1) | 0.6 V (100 kΩ / 150 kΩ divider from 1 V) |
| Cascode gate bias (M2) | 1 V through 100 kΩ, 5.67 pF decoupling |
| Transistor width (M1, M2) | 102 µm each (34 fingers × 3 µm) |
| Drain current | 2.1 mA |
| Load resistor Rd | 200 Ω (in parallel with Ld and Cd) |
| Source inductor Ls | 1 nH |
| Gate inductor Lg | 5.09 nH |
| External Capacitor Cex | 720 fF |
| Drain inductor Ld | 4.73 nH |
| Drain capacitor Cd | 714 fF |
| Channel length L | 45 nm |

## Results (post-layout)

| Metric | Target | Post-layout result |
|---|---|---|
| Noise figure | <5 dB | 2.97 dB |
| S11 | ≤ −20 dB | −30.19 dB |
| Voltage gain | 15–20 dB | 17.99 dB |
| Power consumption | ≤ 2.5 mW | 2.1 mW |
| IIP3 (supplementary) | ≥ −10 dBm (not a primary spec) | −12.36 dBm (did not meet its target) |
| Chip area | n/a | 0.113 mm² |

NF, S11, gain and power all meet their targets. IIP3 was treated as a supplementary metric next to these, and the post-layout result of −12.36 dBm missed the target set for it.

## Design decisions and trade-offs

1. **Why PCSNIM.** PCSNIM adds $C_{ex}$ as an extra degree of freedom. The transistor can be sized small for low power and low noise, while $C_{ex}$ restores the capacitance needed for input matching, easing the noise-matching trade-off of SNIM [1]. The larger total capacitance also lowers the required $L_g$ (5.09 nH here). The cost is extra area from $C_{ex}$ and a resonance that is more sensitive to its value.
2. **$L_g$ cap and inductor area.** $L_g$ is capped at 10 nH. It sits directly in the input path, so its series resistance adds noise at the first stage, and larger on-chip inductors have lower Q. The non-ideality analysis (in the thesis) showed $L_g$ is the dominant source of degradation, so the final design uses 5.09 nH. Inductors also occupy a large share of the silicon area, so every extra nH costs area as well as Q. This is why $C_{ex}$ is preferred over a larger $L_g$.
3. **Bias selection.** In a $V_{gs}$ sweep of the transistor at 2.4 GHz, $\mathrm{NF}_{min}$ is lowest at $V_{gs}$ = 0.7 V (0.168 dB) and rises again at higher bias. At $V_{gs}$ = 0.6 V, $\mathrm{NF}_{min}$ is 0.196 dB, only 0.028 dB higher, while the drain current is about 37% of the current at the optimum. Biasing higher therefore costs power for almost no noise benefit, so $V_{gs}$ is set to 0.6 V. The final 102 µm device (34 fingers × 3 µm) draws 2.1 mA (2.1 mW) at this bias.
4. **Layout parasitics.** Post-layout extraction shifted the schematic results (NF 2.45 dB, S11 −35.09 dB, gain 19.54 dB) to NF 2.97 dB, S11 −30.19 dB and gain 17.99 dB, all within target. In a preliminary extraction, separate R-only and C-only runs showed that resistance dominated the NF increase (+0.5 dB for R only vs. +0.1 dB for C only, relative to the extraction without parasitics). NF stayed within 0.1 dB of the circuit's $\mathrm{NF}_{min}$, so the added noise comes from resistive loss rather than a noise mismatch. S11 also degraded only in the R-only run, where the input reactance moved by about −5 Ω; the C-only run did not degrade it. The 1.55 dB gain drop was not isolated to R or C.
5. **Cascode.** M2 is stacked on M1 to isolate the input from the output, so the input match does not shift easily with the output tank. Without it, $C_{gd}$ of M1 feeds the drain back to the gate, and the Miller effect multiplies it by the stage gain. That changes the effective input capacitance, and with it the resonance and $\mathrm{Re}(Z_{in})$. With M2, the drain of M1 sees roughly $1/g_{m2}$, so the gain of M1 is close to unity and this effect is small. The cost is voltage headroom at a 1 V supply.

## References

1. K. Nguyen, C.-H. Kim, G.-J. Ihm, M.-S. Yang, and S.-G. Lee, "CMOS low-noise amplifier design optimization techniques," *IEEE Trans. Microw. Theory Techn.*, vol. 52, no. 5, pp. 1433–1442, May 2004.
2. B. Razavi, *RF Microelectronics*, 2nd ed. Prentice Hall, 2011.
3. Bluetooth SIG, *Bluetooth Core Specification*, Version 6.0, 2024.

## Not included

Cadence libraries, technology files and raw layout databases. Design was done with gpdk045.
