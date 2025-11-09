# Turbo liquid pump control

This script assumes an analyzer is connected to the output network of the volume pump (when mode is 0).
* If the mode is 0 (default), control the pump setting and disable it when `TARGET_RATIO` is reached (by volume).
* Else (if the mode is 1), stop the pump when the network is empty.

## Pins

0. Analyzer : a liquid/gas analyzer, liquid/gas tank or anything device with allowing to read `Pressure` and `Temperature` of the pipe network to monitore.
1. TurboPump : a Turbo Liquid Volume Pump to control.
2. _Not used_
3. _Not used_
4. _Not used_
5. _Not used_

## Configuration

In the IC script, set `TARGET_RATIO` to the volume ratio to reach (pump will disable once there).
