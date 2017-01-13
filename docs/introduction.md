### Motivation

Upon testing the wonderful *MAN Stadtbusfamilie* add-on after its release in September 2016, I noticed that the vehicles' heating / cooling script suffered from a bug: Its driver's A/C function would cool the bus almost with the intensity of a refrigerator :stuck_out_tongue:. Since it was not the first time I was witnessing the particular bug, I decided to do myself a favor and fix it; *"this shouldn't take more than an hour"*, I thought. Little did I know that I would end up wasting roughly two months rewriting the entire damned thing, polishing and testing it over and over, until it felt good enough to me. Once that "milestone" had been achieved, I wondered whether it would be meaningful to contribute the resulting modification to the add-on's developers directly, or to just publish it for everyone to use. Eventually I chose to follow the latter path, as the script is not particularly tightly coupled to the vehicles it was written for and could thus prove useful to other vehicle (modification) developers in the future.

### Credits

Thank you...
- [M+R Software](http://m-r-software.de/), for giving us the game, scripting engine and the original version of this very script; also for the two *MAN NL/NG* sound files of theirs referenced herein<sup>[1](#footnote-1)</sup>.
- [Chrizzly92](http://www.omnibussimulator.de/forum/index.php?page=User&userID=15380) and everyone having contributed to the [MAN Stadtbusfamilie](http://man-stadtbus.de) add-on, for the awesome buses in general and the derived version of the script in particular.
- [Morphi](http://www.omnibussimulator.de/forum/index.php?page=User&userID=531), for all the years of tireless contributing he has invested into the community on so many levels in general, the two of his *MB O530(G)* mod pack's sound files referenced herein<sup>[1](#footnote-1)</sup>, some ideas as well as a few lines of code that were taken / adopted from his aforementioned mod's respective script.
- [Carl R. Nave](http://hyperphysics.phy-astr.gsu.edu/hbase/Kinetic/relhum.html#c4), [Steve Scanlon](http://www.ringbell.co.uk/info/humid.htm) and [Wolfgang Kühn](http://www.decatur.de/javascript/dew/): the const-file's humidity- and dew point-related "curves" are based on output data that were generated from utilities authored and/or maintained by these people.

### Features

#### Function enhancements

The effectiveness and the start / stop preconditions of all major functions (air-conditioning, cabin heaters, etc.) have been reworked so as to feel more realistic.

#### Sound hooks

Sound hooks pertaining to all major functions have been introduced. Note that you will still have to install sound files of your choosing yourself and couple them with the provided hooks in the sound configuration file of the vehicle you are modding, in order for them to become audible. An example `sound_xxx.cfg` excerpt is given in the [installation](https://github.com/unorthodox-paradox/omsi_2_man_stadtbusfamilie_heating_cooling_script/wiki/Installation#sound-integration) chapter.

#### Window misting hooks

Hooks expressing the degree of window fogging on the outside and inside, based on temperature and humidity, have been added. Like the sound-related variables, these are merely hooks, meaning that you will have to provide and integrate your own fog textures to see the feature in action.

#### Greenhouse-like effect

The cabin can get considerably warmer than its environment, depending on factors such as the time of the day and the season.

#### Humidity management

Vehicles featuring passenger air-conditioning now provide semi-automated humidity management facilities assisting in maintaining the cabin's level of humidity within (marginally) comfortable limits.

#### Structural script changes

The script has received a major refactoring in an effort to increase its modularity. The documentation coverage has slightly improved as well. This is of course more of a developer aid, than a tangible end-user feature.

### Disclaimers

#### Performance consideration

This is a somewhat "performance-intensive" script, partially due to its complexity, but most importantly because of the extensive floating point arithmetic it performs. Therefore, if you decide to use it, you should expect experiencing a *mild* performance degradation (< 5 FPS). As this greatly depends on your hardware and environment (and formal benchmarking is hard, if not outright impossible in OMSI) I cannot be more specific.

#### Correctness

I am neither a physicist, nor someone knowledgeable on the field of heating / cooling systems; in fact I am not even particularly bright at science / math in general (but even if I were, OMSI's not-so-great math support would still get in the way). The script is consequently based on common sense and empirical evidence at large, rather than backed by "hard" science. If you came here in search of something even remotely scientifically accurate, I must disappoint you—you visited the wrong HTTP resource.

***
<sub><a name="footnote-1">1</a>: Those are merely referenced, i.e., they are *not redistributed* with this modification.</sub>
