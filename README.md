# ncp1529asnt1g (prelease, untested)

2.7V-5.5Vin -> 900mV-3.9Vout 1.7MHz 1A Buck Converter

Vout set with assertions, just change the value of OUTPUT_VOLTAGE

## Regulator Module

```
Vfb = 600mV

    INPUT_VOLTAGE: voltage
    VIN_MIN = 2.7V
    VIN_MAX = 5.5V
    assert INPUT_VOLTAGE < VIN_MAX; assert INPUT_VOLTAGE > VIN_MIN

    OUTPUT_VOLTAGE: voltage
    VOUT_MIN = 900mV
    VOUT_MAX = 3.9V
    assert OUTPUT_VOLTAGE < VOUT_MAX; assert OUTPUT_VOLTAGE > VOUT_MIN

    Rtop.resistance = ((OUTPUT_VOLTAGE / Vfb) - 1) * Rbottom.resistance
```

## Usage

```
import ElectricPower
from "eigenlucy/ncp1529asnt1g/main.ato" import Regulator

module App:
    power_batt = new ElectricPower # Connect to battery
    power_3V3 = new ElectricPower # 3V3 rail, supplied by regulator

    ldo = new Regulator
    ldo.OUTPUT_VOLTAGE = 3.3V +/- 5%
    ldo.Vin ~ power_batt
    ldo.Vout ~ power_3V3
```

## TODO

- Solve input cap and output LC filter with assertions
- Solve for Iq and test if within limits

Created by lucy moglia <eigenlucy@proton.me>
