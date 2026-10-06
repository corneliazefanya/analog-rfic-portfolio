# Low-Power 45 nm CMOS LNA for 2.4 GHz BLE Receivers (PCSNIM)

Undergraduate thesis, Universitas Gadjah Mada. Own design, from schematic to post-layout extraction.

## Overview

A low-noise amplifier for the front end of a 2.4 GHz Bluetooth Low Energy receiver, using the PCSNIM technique (power-constrained simultaneous noise and input matching) with inductive source degeneration. Target specifications were derived from the Bluetooth Core Specification 6.0.

Topology progression studied in the thesis: common-source, inductively degenerated common-source, SNIM, then PCSNIM.

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
| Bias voltage Vgs | 0.6 V |
| Transistor fingers (nf) | 34 |
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
| S11 | <= -20 dB | -30.19 dB |
| Voltage gain | 15-20 dB | 17.99 dB |
| Power consumption | ≤2.5 mW | 2.1 mW |
| Chip area | n/a | 0.113 mm^2 |

## Design decisions and trade-offs

1. **Why PCSNIM.** PCSNIM adds $C_{ex}$ as an extra degree of freedom. The transistor can be sized small for low power and low noise, while $C_{ex}$ restores the capacitance needed for input matching, easing the noise-matching trade-off of SNIM. The larger total capacitance also lowers the required $L_g$ (5.09 nH here). The cost is extra area from $C_{ex}$ and a resonance that is more sensitive to its value.
2. **$L_g$ cap and inductor area.** $L_g$ is capped at 10 nH. It sits directly in the input path, so its series resistance adds noise at the first stage, and larger on-chip inductors have lower Q. The non-ideality analysis showed $L_g$ is the dominant source of degradation, so the final design uses 5.09 nH. Inductors also dominate silicon area, so every extra nH costs area as well as Q. This is why $C_{ex}$ is preferred over a larger $L_g$.
3. **Bias selection.** Higher bias current lowers NF$_{min}$, but the gain flattens quickly: NF changes by only 0.028 dB from 1.4 mA to 3.75 mA, while power keeps rising. The bias is therefore set at 1.40 mA ($V_{gs}$ = 0.6 V), where NF is already near its minimum and $g_m$ is sufficient for gain and the 50 Ω match, within the 2.5 mW budget (2.1 mW total).
4. **Layout parasitics.** Post-layout extraction shifted the schematic results (NF 2.45 dB, S11 −35.09 dB, gain 19.54 dB) to NF 2.97 dB, S11 −30.19 dB and gain 17.99 dB, all within target. Separate R-only and C-only extractions show that resistance dominates the NF increase (+[0.5] dB for R only vs. +[0.1] dB for C only, relative to the extraction without parasitics). The gap between NF and NFmin stays below 0.1 dB, so the added noise comes from resistive loss rather than a noise mismatch. The S11 degradation also comes from resistance, which shifts the input reactance by [−5] Ω, while capacitance alone does not degrade it. To reduce the resistive contribution, the input and source routing were shortened and widened, and $L_g$, $C_{ex}$ and $C_d$ were re-tuned after extraction.

   
## References

1. K. Nguyen, C.-H. Kim, G.-J. Ihm, M.-S. Yang, and S.-G. Lee, "CMOS low-noise amplifier design optimization techniques," *IEEE Trans. Microw. Theory Techn.*, vol. 52, no. 5, pp. 1433–1442, May 2004.
2. B. Razavi, *RF Microelectronics*, 2nd ed. Prentice Hall, 2011.
3. Bluetooth SIG, *Bluetooth Core Specification*, Version 6.0, 2024.

## Not included

Cadence libraries, technology files and raw layout databases. Design was done with gpdk045.
