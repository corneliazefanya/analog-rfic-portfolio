# 2.4 GHz Receiver Chain Simulation

RFIC course, Module 2 (Receiver System), 2025. System-level simulation in Cadence Virtuoso / Spectre.

## Scope

Simulation of a receiver chain made of an LNA, mixer, baseband amplifier and oscillator, driven by a testbench. The blocks in this module were provided by the course. The purpose of the module was to build the testbench and verify system behavior. My own LNA is the one in [lna-pcsnim-ble](../lna-pcsnim-ble/).

## What was verified

Transient and FFT analysis along the chain:

| Node | Observation |
|---|---|
| RF input | about 2.4 GHz |
| LNA output | peak at 2.41 GHz |
| Mixer output | downconverted to a 10 MHz IF (LO about 2.4 GHz) |
| Baseband output | 10 MHz |

## Bit-stream decoding

Three input bit streams (PWL sine sources) were recovered from the baseband output waveform by sampling the output and converting the samples to text. All three messages decoded correctly.

_TODO: add one line on how bit timing and sampling points were chosen._

## Images

Add to `images/`:

- [ ] Testbench schematic
- [ ] FFT at LNA output, mixer output and baseband output
- [ ] Transient waveform of the baseband output with sampling points

## Not included

Cadence libraries and provided block designs.
