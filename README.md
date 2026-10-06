# Analog / RF IC Design Portfolio

Cornelia, B.Eng. Electrical Engineering, Universitas Gadjah Mada (UGM).
Focus: RF / analog IC design.

This repository documents my IC design projects from coursework and my undergraduate thesis. All designs were done in Cadence Virtuoso / Spectre with the generic 45 nm PDK (gpdk045). Library files, technology files and raw layout databases are not included, so each project here is documented with schematics, specifications, simulation results and layout screenshots.

I have no industry experience yet. These are academic projects, and none of them has been taped out.

## Projects

| Project | Block | Summary | Level |
|---|---|---|---|
| [LNA with PCSNIM](lna-pcsnim-ble/) | LNA | Low-power 45 nm CMOS LNA for a 2.4 GHz BLE receiver (undergraduate thesis) | Own design, schematic to post-layout |
| [Transimpedance amplifier](tia-transimpedance-amplifier/) | TIA | Design, optimization and layout of a TIA | Own design, DRC/LVS clean |
| [Receiver chain simulation](receiver-chain-simulation/) | System | 2.4 GHz receiver chain: LNA, mixer, baseband amp, oscillator | System-level simulation (Module 2) |
| [Baseband amplifier and integration](baseband-amplifier-integration/) | Baseband amp | Op-amp based baseband amplifier and integration with mixer and LNA | Own baseband amp design (Module 4) |

## Tools

- Cadence Virtuoso (schematic, layout), Spectre (simulation)
- Pegasus (DRC / LVS), Quantus (parasitic extraction)
- PDK: gpdk045 (45 nm generic)

## Notes on scope

- Blocks provided by the course (for example the LNA and mixer in the receiver modules) are labeled as such in each README. The LNA in `lna-pcsnim-ble` is my own thesis design.
- Where a result missed its target, the README says so.

## Contact

Email: corrie.zefanya@gmail.com
