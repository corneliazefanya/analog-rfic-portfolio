# Baseband Amplifier Design and Receiver IC Integration

RFIC course, Module 4, 2025. Own baseband amplifier design, then integration with a mixer and LNA, in Cadence Virtuoso / Spectre (gpdk045).

## Scope

- Designed: a baseband amplifier built around an op-amp with negative feedback.
- Provided by the course: the mixer and LNA blocks used for integration. My own LNA is the one in [lna-pcsnim-ble](../lna-pcsnim-ble/).

## Design targets

| Metric | Target |
|---|---|
| Conversion gain | 30 to 35 dB |
| Bandwidth | 25 to 30 MHz |

## Component values

| Component | Value | Note |
|---|---|---|
| R0, R1 | 6.5 kOhm | Matched to the single balanced mixer input resistance |
| R2 to R5 | 130 kOhm | |
| M1, M2 capacitors | 265.688 fF | Found by iterative optimization |

Simulations used: dcOp, hbac (harmonic balance AC), tran.

## Results

| Configuration | Conversion gain | 3 dB bandwidth | DC power |
|---|---|---|---|
| Baseband amp + mixer | 34.85 dB | 28.13 MHz | 2.707 mW |
| Baseband amp + mixer + LNA | 54.49 dB | 28.33 MHz | 7.971 mW |

## Analysis

- Loading effect: connecting the baseband amplifier shifted the mixer-side bandwidth from 26.99 MHz to 40.75 MHz.
- Power rose after integration, as expected, with the LNA adding to the total.

_TODO: one sentence on why the amplifier changes the mixer-side bandwidth, in your own words._

## Images

Add to `images/`:

- [ ] Baseband amplifier schematic
- [ ] hbac gain and bandwidth plot (amp + mixer)
- [ ] hbac plot after adding the LNA
- [ ] Integrated receiver schematic

## Not included

Cadence libraries and provided block designs.
