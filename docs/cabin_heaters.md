## Cabin heaters
***
### Definitions

Abbreviation | Meaning
------------ | -------
*FX* | Function label, as per the [overview](./manual.md#overview).

### Introduction

This function controls the cabin heaters, which employ water heated up by the engine and/or *[F4](./auxiliary_heating.md)* to heat up the cabin's passenger area. It is by far the most effective of all active heating functions.

### Effectiveness

The following list enumerates the factors affecting the function's performance:
* The engine's temperature is used to determine F5's output temperature.
* A (statically defined) performance factor affects F5's output volume.
* When F4 is active, the engine's temperature is lower than a maximum limiting value, and the environment is as well colder than (a different) maximum limiting value, F5's output volume is significantly (artificially) increased further so as to boost the heating rate initially. The function is said to operate *turbo profile* when in this state.

### Humidity management coupling

In vehicles not having a roof-mounted A/C unit, a [mutual coupling](./humidity_management.md#activation-profile-and-ac-based-heating--cooling-function-coupling) between this function and *F3* exists. When both functions are active, F5 takes precedence. 

See also: [F5 vs F3 in CM](./humidity_management.md#f5-vs-f3-in-cm)

### Sounds

A single sound is used by F5, the volume of which depends on the output volume.

### Inertia

F5's activation delay depends on the engine's temperature's negative departure from a minimum positive value considered "normal", as well as on a random signal propagation delay; its deactivation delay is entirely random.

Note that, as far as deactivation delay is concerned, the cabin heaters *themselves*, rather than F5 (and potentially F3) controlling them, feature an additional kind of post-deactivation inertia, which, upon deactivation of both of the aforementioned functions, imposes significant delays concerning:
* the return of the heaters' output temperature to the temperature of the cabin, and
* the drop of the heater's output volume to zero.

What this practically means is that the cabin heaters will continue to radiate heat, and thus potentially continue positively contributing to the cabin temperature, for up to several minutes (assuming default values of related constants) following their controlling functions' deactivation. If this behavior seems strange to you, just think of traditional real-world heaters connected to a building's (water-based) central heating system, where this "phenomenon" is in fact even more intense and prolonged than the one simulated by the script.

See also: [F1 / F2 - Cabin heater coupling](./driver_passenger_ac.md#cabin-heater-coupling)

### Idle states

F3 is considered idle when, in addition to its controller being in the "ON" state, any of the following hold:
* The cabin temperature has exceeded the function's *maximum temperature* limit.
* The engine has not yet warmed up sufficiently.
* The engine is not running, the master electrics switch is off or the battery is depleted.

Note that sound playback will only cease once both F3 *and* F5, if applicable, enter an idle or disabled state.
