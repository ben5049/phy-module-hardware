# PHY Module Errata

## Contents

- [1 10BASE-T1S PHY Module v1 Errata](#1-10base-t1s-phy-module-v1)
    - [1.1 MCU NRST Low when 3V3 supply removed](#11-mcu-nrst-low-when-3v3-supply-removed)
- [2 1000BASE-T1 PHY Module v1 Errata](#2-1000base-t1-phy-module-v1)
    - [2.1 MCU NRST Low when 3V3 supply removed](#21-mcu-nrst-low-when-3v3-supply-removed)


## Key

- A = limitation present, workaround available
- N = limitation present, no workaround available
- P = limitation present, partial workaround available
- "-" = limitation absent

## 1 10BASE-T1S PHY Module v1

| **Bug**                                                                          | **1.0.2** | **1.1.0** |
|----------------------------------------------------------------------------------|-----------|-----------|
| [MCU NRST Low when 3V3 supply removed](#11-mcu-nrst-low-when-3v3-supply-removed) | P         | -         |

### 1.1 MCU NRST Low when 3V3 supply removed

The MCU `RST` pin (`+3V3_AON` domain) is connected to the PHY `RST` pin (`+3V3` domain). When `+3V3_AON` is present and `+3V3` is not (sleep mode), the MCU is held in reset due to a current going through the PHY `RST` pullup resistor and internal IO protection diode. This means the MCU sleep mode is non-functional, and the full `+3V3` supply must be provided to program the module.

This was fixed by adding an NMOS in version 1.1.0.

A partial fix for version 1.0.2 is to add a 1k ohm pullup resistor between `+3V3_AON` and MCU `RST`, however this may draw a large current from the PHY `RST` internal IO protection diode.


## 2 1000BASE-T1 PHY Module v1

| **Bug**                                                                          | **1.0.0** | **1.1.0** |
|----------------------------------------------------------------------------------|-----------|-----------|
| [MCU NRST Low when 3V3 supply removed](#21-mcu-nrst-low-when-3v3-supply-removed) | P         | -         |

### 2.1 MCU NRST Low when 3V3 supply removed

See [1.1 MCU NRST Low when 3V3 supply removed](#11-mcu-nrst-low-when-3v3-supply-removed)
