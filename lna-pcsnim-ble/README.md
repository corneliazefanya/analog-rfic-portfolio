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
| Source inductor Ls | 950 pH |
| Transistor fingers (nf) | 34 |

Full device sizes, bias and component values: _TODO: fill from thesis Bab 5_

## Results (post-layout)

| Metric | Target | Post-layout result |
|---|---|---|
| Noise figure | _TODO_ | 2.97 dB |
| S11 | <= -20 dB | -30.19 dB |
| Voltage gain | _TODO_ | about 18 dB |
| Power consumption | _TODO_ | 2.1 mW |
| Chip area | n/a | 0.113 mm^2 |

Notes:

- Gain is reported as voltage gain into a 5 kOhm load rather than S21, because the intended load is a mixer input of about 5 kOhm.
- IIP3 is treated as a supplementary metric. 

## Images

- [ ] LNA Schematic
- [ ] Layout screenshot
- [ ] S11 plot
- [ ] NF plot
- [ ] Gain plot
- [ ] Pegasus DRC / LVS result screenshot

## Design decisions and trade-offs

_TODO: 4 to 6 bullets in your own words. Suggested topics:_

- Why PCSNIM over SNIM for this power budget
- Why Ls = 950 pH and nf = 34 (and how it relates to the parametric sweep)
- How layout parasitics changed NF, S11 and gain compared to the schematic
- What you would change to recover IIP3

## References

- Nguyen et al., 2004
- B. Razavi, RF Microelectronics
- Shaeffer and Lee, 1997
- Bluetooth Core Specification 6.0

## Not included

Cadence libraries, technology files and raw layout databases. Design was done with gpdk045.
