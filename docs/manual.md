## Manual
***
This chapter provides details on the functionality offered by the script, as well as usage and customization information.

It should be noted that, while effort has been put into making the discussion of each topic reasonably comprehensive, the script and its accompanying files remain the sole definitive source of information at all times. Formulated otherwise, this page and its linked ones are *not* destined to cover every detail and corner case there is, simply because, if this were the case, the resulting documentation would be harder to decipher than the script itself.

Terminology note: The recurring phrase *"(when) in a heating / cooling / dehumidification / humidification context..."* is to be interpreted as *"in a situation where a heating / cooling / dehumidification / humidification effect is desired (more than anything else, i.e., being the user's first priority), then..."*.

### Functions

A *function* is any simulated functionality pertaining to the vehicle or the environment and affecting the former's temperature and/or humidity in some manner. This section focuses on the most important ones among the functions, stating their respective purpose, discussing some of the factors affecting them, and providing practical examples and guidelines along the way.

#### Active functions

*Active functions* are user-controlled, i.e., functions which the user (virtual driver) can influence. This section will specifically center around the functions of this kind that are to some extent controllable via the heating / cooling panel (extended by the cabin heaters controller which, for reasons unknown to me, always seems to be allocated an external "slot").

Active functions may have *attributes*—"sub-functions" (for lack of a better term, in the sense that they do not per se contribute heat) that modify the way the functions they are associated with operate. While on a technical level everything is of course interconnected at some degree, attributes' relationships with functions extend beyond that, being more "business contract-like", reaching closer to the physical realm. In more practical terms, attributes express (assumed) real-world, circuit-level couplings, rather than implicit or merely artificial script-level connections or dependencies. Functions and attributes have a *many-to-many* relationship. To confuse matters further, functions can themselves act as other functions' attributes.

A central function-related aspect that the script addresses extensively is the notion of *inertia*, which within this scope could be described as being the time required for a change in a function's state to become effective, or, perhaps better formulated, the time required for the function to bring about (observable) system-wide change. The reason why this is mentioned vaguely at this point is to serve as a subtle but general reminder to readers who might be concerned that a function is flawed simply because it induces no *instant* noticeable temperature change—worry not, it may take from seconds up to several minutes, depending on the context, for that to happen.

##### Overview

The screenshot below summarizes the functions and attributes that are to be discussed in this section; the (regular expression) notation `[FA]\d(\:\s\{F\d(,\sF\d)*\})?` in the bordered boxes enclosing the buttons is to be interpreted as *"the attribute or function identified by this digit acts as an attribute of these functions"*.

![heating-panel](http://i.imgur.com/mJpNQrm.png)

The next table summarizes the same information, also providing links to each active function's dedicated documentation page (attributes or functions acting as attributes have no pages of their own but are instead covered in the sections of the functions *they act upon*).

Function or attribute | Name | Attribute of
--------------------- | ---- | ---------------
*A1*<sup>[1](#function_table_remark_1)</sup> | Air dispensation mode | *F1*
*A2* | Temperature | *F1*
*A3* | Fan speed | *F1*
*A4* | Air circulation mode | *F1*, *F2*
*F1* | [Driver's A/C](./driver_passenger_ac.md) | *F3*<sup>[2](#function_table_remark-2)</sup>
*F2*<sup>[2](#function_table_remark_2)</sup> | [Passengers' A/C](./driver_passenger_ac.md) | *F3*<sup>[2](#function_table_remark_2)</sup>
*F3* | [Humidity management](./humidity_management.md) | *F5*<sup>[3](#function_table_remark_3)</sup>
*F4* | [Auxiliary heating](./auxiliary_heating.md) | *F5*
*F5* | [Cabin heaters](./cabin_heaters.md) | *F1*, *F2*<sup>[2](#function_table_remark_2)</sup>, *F3*<sup>[3](#function_table_remark_3)</sup>

<sub><a name="function_table_remark_1">1</a>: Not implemented - does nothing.</sub><br/>
<sub><a name="function_table_remark_2">2</a>: Only in vehicles having a roof-mounted A/C unit.</sub><br/>
<sub><a name="function_table_remark_3">3</a>: Only in vehicles without a roof-mounted A/C unit.</sub>

#### Passive functions

*Passive functions* are functions that the user has no (direct) control over. While several such functions are implemented by the script, the sole one of them that is, due to being somewhat new to OMSI-land, worth taking a closer look at, is that of the [greenhouse effect](./greenhouse_effect.md) (abbreviated *GhE* herein).

#### Miscellaneous functionality

This section links to secondary features that do not affect the vehicle's temperature or humidity.

##### [Window misting effect](./window_misting_effect.md) *(WME)*

### Common use cases

This section serves as a *TL;DR*, providing some practical examples / guidelines to those readers feeling disinclined to read this entire page.

#### Cooling the vehicle

Use [F1](./driver_passenger_ac.md) in *AM*, adjusting A2 and A3 as needed, combined with [F2](./driver_passenger_ac.md). Also, *unless* the cabin is *colder* than the environment, it actually helps keeping windows, hatches and, if possible, doors *open*.

#### Heating the vehicle

When it is *moderately* or *severely* cold outside, use [F5](./cabin_heaters.md) combined with F1 in *EM*, adjusting A2 and A3 as needed. You can additionally use [F4](./auxiliary_heating.md) to speed up F5's start-up time and, if available in *AM*, [F3](./humidity_management.md), so as to prevent the air inside from drying out too much.

When it is just *mildly* cold to neutral outside, you can either use F1 (in either operational mode) and/or F2, or leverage the engine, as well as, potentially, the [GhE](./greenhouse_effect.md), as an implicit "heat source"; the latter two combined, if given some time, can increase the cabin's temperature by several degrees, even during the winter.

#### Dehumidifying the vehicle

When dehumidification is your primary concern, your options are as follows:
* Use F3 if available in AM.
* Use F5 if temperature constraints permit it.
* If the air outside is *drier* than the air inside—typically being the case in a cooling context—, allow cabin - environment air exchange by:
    * Opening windows, hatches, and doors.
    * Using F1 and/or F2 in AM, and *A4* set to *FM*.
* Otherwise reduce air exchange by:
    * Closing windows, hatches, and doors.
    * Disabling F1 and F2 if possible, or at least switch A4 to *RM*.

These approaches should also help demist windows that are fogged on the *interior* side.

#### Humidifying the vehicle

When humidification is your primary concern, your options are as follows:
* Use F3 is available in AM.
* Disable any heat-contributing function you may be using, if temperature constraints permit doing so.
* If the air outside is *more moist* than the air inside—typically occurring in a heating context—, allow cabin - environment air exchange by:
    * Opening windows, hatches, and doors.
    * Using F1 and/or F2 in AM, and A4 set to FM.
* Otherwise reduce air exchange by:
    * Closing windows, hatches, and doors.
    * Disabling F1 and F2 if possible, or at least switch A4 to RM.

### Technical documentation / Reference

This last section quickly goes over the internal workings of the script and presents some of its customization facilities.

#### Overview

Terminology note: A *script-level function* is any portion of the script (typically spanning one or more macros) that implements (a subset of) the functionality pertaining to one or several of the high-level vehicle aspects discussed up to this point. For the sake of clarity, the latter will for the remainder of this page be referred to as *features*. There is no precise mapping between script-level functions and corresponding features; features have really only been employed thus far as a necessary oversimplification to facilitate the process of explaining in a straightforward manner to readers not familiar with OMSI's scripting language what it is the script (roughly) does.

The basic structure of the original M+R script has been maintained. For each script-level function, the primary macro, `cabinair_frame`, delegates to the appropriate macros in order to:
* Evaluate whether a function is "active", i.e., in this context, if preconditions hold for it to bring about change to system state.
* Calculate, based on the above evaluation, the function's delta (change or rate of change) or some variable portion thereof.
* Determine, for sound-emitting functions, the sound volume.

Lastly the delegator computes the final values that (measurable) system state comprises, by combining as appropriate their initial values with their corresponding deltas returned by the respective delegates. For example, in the case of cabin temperature, the overall difference from the cabin temperature the frame before is simply the summation of the temperature rates of all functions that affect temperature.

#### Variables of potential interest

The following variables might be of some value to other scripts. Note that reassigning any of them externally will likely cause this script to break, unless you know what you are doing.

Variable | Purpose | Unit | Values
-------- | ------- | ---- | ------
`(driver|passenger)_ac_t(_target)?` | Current / Target F1 / F2 output temperature. | °C |
`cabinair_Vrate_(driver|passenger)_ac(_target)?` | Current / Target F1 / F2 output volume rate. | m<sup>3</sup>/s | ≥ 0
`cabinair_Vrate_(driver|passenger)_ac_humidity` | Current F1 / F2 humidity-relevant output volume rate. | m<sup>3</sup>/s | ≥ 0
`cabinair_Qrate_(driver|passenger)_ac` | Current F1 / F2 temperature rate. | °C/s |
`(driver|passenger)_ac_start_stop_delay` | Aggregate F1 / F2 start / stop delay. | s | -1 = no state transition pending<br/>≥ 0 otherwise
`(driver|passenger)_ac_running(_target)?` | Current / Target F1 / F2 status. | | -1 = pre-heating/-cooling<br/>0 = stopped or running in maintenance<br/>1 = running normally<br/>2 = running in eco
`(((driver|passenger)_ac_(fan|int))|(ac_ext))_sound_vol(_target)?` | Current / Target F1 / F2 fan or interior A/C sound volume, or volume of sound emitted by roof-mounted A/C unit. | | [0, 1]
`auto_humidity_management` | Whether F3 is active in AM / AS-AP. | |  boolean
`ac_humidity_management_active` | Whether F3 is active in AM, regardless of the AP in effect. | | boolean
`auto_humidity_management_start_stop_delay` | Aggregate start / stop delay of F3 in AM. | s | -1 = no state transition pending<br/>≥ 0 otherwise
`cabin_heater_dehumidification_active` | Whether F3 is active in CM. | | boolean
`auxheat_active` | Whether F4 is active. | | boolean
`auxheat_start_stop_delay` | Aggregate F4 start / stop delay. | s | -1 = no state transition pending<br/>≥ 0 otherwise
`auxheat_sound_vol(_target)?` | Current / Target F4 sound volume. | | [0, 1]
`cabin_heater_t(_target)?` | Current / Target F5 output temperature. | °C |
`cabinair_Vrate_cabin_heater(_target)?` | Current / Target F5 output volume. | m<sup>3</sup>/s | ≥ 0
`cabin_heaters_running(_target)?` | Current / Target F5 status. | | boolean
`cabin_heaters_start_stop_delay` | Aggregate F5 (or F3 in CM) start / stop delay. | s | -1 = no state transition pending<br/>≥ 0 otherwise
`cabin_heaters_sound_vol(_target)?` | Current / Target F5 sound volume. | | [0, 1]
`cabinair_Qrate_ghe(_plus_losses)?` | Net / pure GhE temperature increase rate. | °C/s | ≥ 0
`(env|cabin)_dew_point` | A rough estimate of the environment's / cabin's dew point, relied upon by the WME's implementation. | °C |
`env_rel_humidity` | A rough estimate of the environment's relative humidity. | °C | (0, 1)
`cabin_window_(int|ext)_misting(_target)?` | Current / Target WME degree on the outside / inside. | | [0, 1]

#### Constants of potential interest

The following constants are among the most significant; several more are available.

Constant | Purpose | Unit | (Recommended) Values
-------- | ------- | ---- | --------------------
`cabinair_V` | The cabin's air's volume; *every* function's but *F4*'s effectiveness is *inversely proportional* to this value.| m<sup>3</sup> | > 0
`cabinair_A_(driver|passenger)_ac` | F1's / F2's area of air exchange. | m<sup>2</sup> | > 0
`driver_ac_min_selectable_t` | A2's minimum temperature setting. | °C | > 0
`driver_ac_min_max_selectable_t_interval` | A2's minimum - maximum temperature setting interval. | °C | > 0
`ac_cooling_cabin_t_min` | No cooling will take place by F1 (in AM) / F2 if the cabin is *colder* than that. | °C | 
`ac_cooling_output_t_min` | Minimum output temperature the A/C unit can attain. | °C |
`ac_cooling_loss_per_degree` | Efficiency drop of the A/C unit per degree of F1's (in AM) / F2's target output temperature's departure from current environment (A4 in FM) or cabin (A4 in RM) temperature in a *cooling* context. | | (0, 1)
`ac_heating_cabin_t_max` | No heating will take place by F1 (in AM) / F2 if the cabin is *warmer* than that. | °C |
`ac_heating_output_t_max` | Maximum output temperature the A/C unit can attain. | °C |
`ac_heating_loss_per_degree` | Efficiency drop of the A/C unit per degree of F1's (in AM) / F2's target output temperature's departure from current environment (A4 in FM) or cabin (A4 in RM) temperature in a *heating* context. | | (0, 1)
`(driver|passenger)_ac_effectiveness` | Multiplied by<br/>`cabinair_A_(driver|passenger)_ac`<br/>to artificially decrease (when < 1) or increase (when > 1) F1's / F2's effectiveness, without affecting corresponding output temperatures. | | > 0
`number_of_passenger_ac_units` | Same as `(driver|passenger)_ac_effectiveness`. | | integer > 0
`auto_humidity_management_dehumidification_start_rel_cabin_humidity_max` | F3 in AM / AS-AP will only get triggered for *dehumidification* when the cabin's *relative* humidity *exceeds* this threshold. | | (0, 1)
`auto_humidity_management_humidification_start_rel_cabin_humidity_min` | F3 in AM / AS-AP will stop *dehumidifying* the cabin's air when its *relative* humidity falls *below* this limit. | | (0, 1)
`auto_humidity_management_dehumidification_stop_rel_cabin_humidity_min` | F3 in AM / AS-AP will only get triggered for *humidification* when the cabin's *relative* humidity is *lower* than this threshold. | | (0, 1)
`auto_humidity_management_humidification_stop_rel_cabin_humidity_max` | F3 in AM / AS-AP will stop *humidifying* the cabin's air when its *relative* humidity *exceeds* this limit. | | (0, 1)
`dehumidification_cabin_rel_humidity_min` | F3 in CM or AM / MS-AP will stop *dehumidifying* the cabin's air when its *relative* humidity falls *below* this limit. | | (0, 1)    
`humidification_cabin_rel_humidity_max` | F3 in CM or AM / MS-AP will stop *humidifying* the cabin's air when its *relative* humidity *exceeds* this limit. | | (0, 1)
`dehumidification_effectiveness` | F3 in AM will decrease the cabin's *relative* humidity at this *ideal* rate. | | (0, 1)
`humidification_effectiveness` | F3 in AM will increase the cabin's *relative* humidify at this *ideal* rate. | | (0, 1)
`heizung_Qrate_auxheat` | Rate at which F4 heats the engine. | J/s | > 0
`auxheat_engine_t_max` | F4 will stop heating the engine once the latter's temperature exceeds this value. | °C | > 0
`cabinair_A_cabin_heater` | F5's area of air exchange. | m<sup>2</sup> | > 0
`cabin_heater_cabin_t_max` | No heating will take place by F5 (or F3 in CM) if the cabin is warmer than that. | °C | > 0
`cabin_heater_engine_t_min` | F5 (or F3 in CM) will refuse to start unless the engine is warmer than that. | °C | > 0
`number_of_cabin_heaters` | Multiplied by `cabinair_A_cabin_heater` to produce the overall area. | | integer > 0
`cabin_heater_turbo_mode_env_t_max` | F5 (or F3 in CM) turbo profile environmental temperature precondition. | °C |
`cabin_heater_turbo_mode_engine_t_max` | F5 (or F3 in CM) turbo profile environmental temperature precondition. | °C | > 0
`cabin_heater_turbo_mode_effectiveness_increase_factor` | Multiplied by `cabinair_A_cabin_heater` to artificially decrease (when < 0) or increase (when > 0) the function's effectiveness, without affecting its output temperature.  | > 0
`cabin_heater_effectiveness` | Same as above, but used regardless of turbo profile. | > 0
`ghe_t_increase_rate_max` | Maximum (pure) GhE-induced cabin temperature increase rate. | °C/s | > 0
`ghe_time_max` | Maximum time period throughout which `cabinair_Qrate_ghe` will apply. The overall GhE heating effect thus is `cabinair_Qrate_ghe` * `ghe_time_max` | > 0
`cabin_window_misting_rel_humidity_min` | WME relative environment / cabin humidity precondition. | | (0, 1)

#### Macros of potential interest

Whether you have found yourself in a dead-end, due to none of the exposed constants enabling you to adapt the script's functionality sufficiently so that it satisfies your requirements, thus being forced to modify the script itself, or just seek further information, consider visiting the macros enumerated below as a first step:

Macro | Purpose
----- | -------
`cabinair_frame` | The primary macro that calls all others and combines their output.
`calculate_(driver|passenger)_ac_temps` | Calculates F1's / F2's output temperature.
`actualize_(driver|passenger)_ac_status` | Activates or deactivates F1 / F2.
`calculate_(driver|passenger)_ac_air_exchange_volumes` | Calculates F1's / F2's output air / humidity volume.
`actualize_(driver|passenger|ext)_ac_sound` | Determines F1's / F2's fan / interior A/C sound volume or the volume of the sound emitted by the roof-mounted A/C unit.
`actualize_auto_humidity_management_status` | Signals activation or deactivation of F3 in AM / AS-AP to the macro below.
`actualize_ac_humidity_management_status` | Enables or disables F3 in AM.
`actualize_auxheat_status` | Activates or deactivates F4.
`calculate_cabin_heater_temps` | Calculates F5's output temperature.
`actualize_cabin_heater_status` | Activates or deactivates F5.
`actualize_cabin_heater_sound` | Determines the cabin heaters' (thus also F3's, potentially) sound volume.
`ghe_impact` | Calculates GhE's temperature rate.
`calculate_cabin_window_(int|ext)_misting_degree` | Calculates the degree of window fogging on the inside / outside.
