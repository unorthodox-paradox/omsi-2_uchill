## Auxiliary heating
***
### Definitions

Abbreviation | Meaning
------------ | -------
*FX* | Function labels, as per the [overview](./manual.md#overview).

### Introduction

This function interfaces with an (imaginary) auxiliary power unit to pre-heat the engine, as well as the water—which is normally engine-heated—employed by [F5](./cabin_heaters.md), in order to, in the former case, assist ignition, as well as, in the latter, boost F5's initial effectiveness, under cold environmental conditions. When active, F4 also minimally and implicitly heats the cabin itself (actually the engine itself does, as a result of being--due to this function and/or normal operation--warmer than the cabin).

### Effectiveness

F4's effectiveness is proportional to the environmental temperature and the engine's volume; the second factor falls outside of this script's responsibilities, as it is the engine script that affects it.

### Sounds

F4 uses a single sound, whose maximum sound volume is statically defined.

### Inertia

F4's activation delay depends on the engine's temperature's negative departure from a minimum positive value considered "normal", as well as on a random signal propagation delay; its deactivation delay is entirely random.

### Idle states

When the function's controller's LED is in a blinking state, F4 is either in the process of starting up, or inactive because its targeted engine temperature—which is statically defined—has been achieved.
