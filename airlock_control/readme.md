# Airlock control

This setup expects one or more airlocks (up to six), each one having a dedicated IC10.
In case of several airlocks, a central command IC can be used to mirror the airlocks states (ie. when open is open, all the other open too).

## Airlock IC

This IC is in charge of one airlock with sandard elements:
- Two doors,
- Two active vents,
- One gas sensor.

When using a central command IC, the last pin is connected to this IC (or a miror).
If last pin is not set, the airlock works locally and the code disregard commands related the the central command.

The IC works as a state machine with the following states:
- **INTERN_OPEN**
   * Internal door is opened,
   * External door is closed,
   * Internal vent is off,
   * External vent is off,
   * Internal Setting is reset unless a button is pressed.
  On door activation:
   * Internal Setting is set to 1,
   * Transition to INTERN_TO_EXTERN.
  If internal Setting is different than the central control:
   * Transition to INTERN_TO_EXTERN.
- **INTERN_TO_EXTERN**
   * Internal door is closed,
   * External door is closed,
   * Internal vent is on,
   * External vent is off.
  When pressure is null:
   * Transition to EXTERN_OPEN.
- **EXTERN_OPEN**
   * Internal door is closed,
   * External door is opened,
   * Internal vent is off,
   * External vent is off,
   * Internal Setting is reset unless a button is pressed.
  On door activation:
   * Internal Setting is set to 1,
   * Transition to EXTERN_TO_INTERN.
  If internal Setting is different than the central control:
   * Transition to INTERN_TO_EXTERN.
- **EXTERN_TO_INTERN**
   * Internal door is closed,
   * External door is closed,
   * Internal vent is off,
   * External vent is on.
  When pressure is null:
   * Transition to INTERN_OPEN.

## Central control IC

This IC pins are connected to each airlock IC (or a miror).
* Its internal Setting represents the state all other airlocks must follow.
  The central IC transition from states INTERN_OPEN to state EXTERN_OPEN only (it never use the states INTERN_TO_EXTERN and EXTERN_TO_INTERN).
* Each tick, it checks all connected devices Setting and, if one is set, the central control state (Internal Setting)
  is transitionned.
