# Heater control

* Enable or disable connected heaters if temperature falls under the target temperature.
* Disable the heater when there is no pressure.

## Pins

0. Analyzer : a liquid/gas analyzer, liquid/gas tank or anything device with allowing to read `Pressure` and `Temperature` of the pipe network to monitore.
1. Heater_1 : a pipe heater connected to the pipe network to monitore.
2. Heater_2 (facultative) : a pipe heater connected to the pipe network to monitore.
3. Heater_3 (facultative) : a pipe heater connected to the pipe network to monitore.
4. _Not used_
5. _Not used_

## Configuration

* In the IC script, set `TARGET_TEMP` to the minimum temperature in the pipe network (in Kelvins).
  If the pipe network reaches this temperature, heaters activate.
