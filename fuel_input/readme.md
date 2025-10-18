## SUmmary

Control pumps to fill a target pipe network with O2 and H2 up to a pre-defined pressure.

## Devices

* AnalyzerTarget (d0): a pipe analyzer on the target pipe network
* PumpH2 (d1): (turbo)-pump with input connected to an H2 tank/network and output connected to the target pipe network
* PumpH2 (d2): (turbo)-pump with input connected to an O2 tank/network and output connected to the target pipe network

## Constants

* TARGET_PRESSURE_H2: target H2 pressure in Pa - the script will try to reach this pressure, but may overshoot a bit
* TARGET_PRESSURE_O2: target O2 pressure in Pa - the script will try to reach this pressure, but may overshoot a bit
* PUMP_SPEED_H2: a constant controling the speed of the H2 pump - the higher it is, the faster H2 is pumped and the bigger overshoot will be
* PUMP_SPEED_O2: a constant controling the speed of the O2 pump - the higher it is, the faster O2 is pumped and the bigger overshoot will be
