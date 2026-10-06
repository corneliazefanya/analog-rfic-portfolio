# Transimpedance Amplifier (TIA)

Analog IC course module, 2025. Design, optimization and layout in Cadence Virtuoso with gpdk045.

## Overview

A transimpedance amplifier optimized against gain, bandwidth, power and output DC level specifications, followed by layout with a clean DRC and LVS.

_TODO: add the topology description (for example the amplifier structure and feedback element) from the report._

## Specifications and results

| Metric | Spec | Result |
|---|---|---|
| Gain | 57 to 58 dB | 57.56 dB |
| 3 dB bandwidth | > 4 MHz | 4.25 MHz |
| DC power | < 1 mW | 471.8 uW |
| DC output voltage | 0.7 to 1.1 V | 1.064 V |

## Optimization

Design variables were tuned from initial to final values:

| Variable | Initial | Final |
|---|---|---|
| LF | 1.6u | 0.95u |
| LR1 | 10u | 18u |
| LR2 | 5u | 5u |
| NF1 | 16 | 10 |
| NF2 | 4 | 10 |

## Analysis

The report analyzes the gain versus bandwidth trade-off through the Miller effect on Cgd.

_TODO: 2 to 3 sentences summarizing the argument and what limited bandwidth in your design._

## Layout and verification

- Pegasus DRC: 0 violations out of 562 checks
- LVS: clean
- _TODO: layout area, if you recorded it_

## Images

Add to `images/`:

- [ ] Schematic
- [ ] AC response (gain and bandwidth)
- [ ] DC operating point / output level
- [ ] Layout screenshot
- [ ] DRC and LVS result screenshots

## Not included

Cadence libraries, technology files and raw layout databases. Design was done with gpdk045.
