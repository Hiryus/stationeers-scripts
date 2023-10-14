# Combustion centrifuge controler

This script controls a [combustion centrifuge](https://stationeers-wiki.com/Combustion_Centrifuge) fueled by NOS.

It gradually increase the centrifuge trhottle and limiter levers to inrease RPM with blocking the machine by controlling the stress value with a [PID](https://en.wikipedia.org/wiki/Proportional%E2%80%93integral%E2%80%93derivative_controller) algorithm.
When the centrifuge reaches 1000 RPM (or more), fixed values (50% / 100%) are applied to decrease fuel consumption.


## Instruction

* Flash the code on an integrated circuit and put it inside the centrifuge IC slot.
* Put a gas mixer with a 50/50 ratio of Volatiles and N2O gas as input to the centrifuge.
  **Warning**: NOS is very unstable and will auto-ignite at 50°C. Make sure to control temperature and pressure.
* Set the first pin of the IC slot to the mixer.
* Start the machine.


## Implementation details (PID)

Only the throttle command is controlled by PID and is noted `U(t)`, or simply `U`.
```
U(t) = Kp * error(t)   +   Ki * integral[0,t](error(t))   -   Kd * delta_error(t)/dt
U = Kp*error + Ki*sum_error - Kd*delta_error
U = Up       + Ui           - Ud
```
Where:
* `error = target_stress - current_stress`,
* `delta_error = last_error - current_error`,
* `sum_error` is the sum of errors over time.

Note: since `error = target_stress - current_stress`, `delta_error` can be rewritten as:
```
delta_error = last_error - current_error
            = (target_stress - last_stress) - (target_stress - current_stress)
            = current_stress - last_stress
```

The limiter command is simpler and siumply proprtional to the current RPM:
```
limiter_cmd = LIMITER_FACTOR * (RPM - LIMITER_MIN_RPM)
```
Where:
* `LIMITER_FACTOR` is a constant,
* `RPM` is the current RPM of the centrifuge,
* `LIMITER_MIN_RPM` is the minimum RPM value to reach before increasing the limiter command.
