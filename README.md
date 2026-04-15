# Hourglass Twins Keyboard
### in 2021, [9% of Americans](https://doi.org/10.15620/cdc:129848) (~30 million people) experienced a repetitive strain injury
Constant typing in an office setting was found to be a significant risk factor. A key reason why is the keyboards many officeworkers use - the standard 104 key ANSI layout was not designed with people in mind. This project aims to implement strategic, ergonomic design choices that improve comfort during typing and decrease the risk of repetitive strain injury.

## Ergonomics
The Hourglass Twins Keyboard implments, among others, 3 key design choices - a column (rather than the standard row) stagger, a thumb cluster, and angled offsets measured specifically to the average male hand size. However, this design is not without compromise; the slim layout would be a dealbreaker for many, as this keyboard only has 38 keys (though through the use of layers, there are actually 38x3=114 effective keys). The main goal of the keyboard is to unite the design and layout of the keys to the physical shape of the human hand, in positions that are comfortable to hold.

A key design goal of this keyboard was that no finger should have to move more than 1 key away to access the keys assigned to it. This, combined with the limted range of motion of the pink restricts the four main fingers to only 15 keys (the index finger gets 2 dedicated columns). The thumbs of each hand get 4 keys because it can swing wide, leading to an overall design of 19 keys per hand, or 38 total.
### Column Stagger
Typical keyboards have their rows offset from eachother. Some claim this is a vestige of typewriter design, but that source is not entirely accurate. This project uses a column stagger, where columns have different heights. This is because our finger lengths naturally vary, and it doesn't make sense to place the home row for the pinky at the same level for the middle finger.
### Angled Column Offset
Try extending your hand from a fist to palm-flat - notice how your fingers _aren't_ parallel? Even many ergonomic keyboards like to assume they are, but this one doesn't. The pinky and ring finger columns both angle away from the central cluster because that's how those fingers look on a hand. Pressing a top key with the pinky is far more comfortable if it just has to extend along its own axis.
### Thumb Cluster
The ANSI layout reserves almost 20% of the hand's fingers for one key: the spacebar. The thumb rarely presses  anything else on a standard keyboard. So, this keyboard utilizes the thumbs extensive range of motion with a comfortable thumb cluster positioned at the center of the board.


## Design
### Layers
Though noted in the paper that Dvorak should be used, further research into the topic reveals there are significantly more advancements to be made. This repo can be forked and the config file edited to match a more standard layout if desired.

The current layer is noted on the e-ink display on the left-half board.
| Layer | Access Key |  Mode | Details |
| -- | -- | -- | -- |
| Alpha | None | Default | Currently using a modified version of the [Caster Layout](https://cyanophage.github.io/#caster). |
| Symbol | Leftmost thumbkey of right-cluster | Hold | Alpha keys are overwritten with symbols such as !@#$%^&*() |
| Number | Rightmost thumbkey of left-cluster | Hold | Alpha keys are overwritten with a numpad on the right board and nav keys on the left board |
| QWERTY (game) | Symbol + Number layer keys at the same time| Toggle | Contains a QWERTY mode on the left-half, with an arragement o `F` keys on the right half. The configuration layer can be accessed from here |
| Config | Rightmost thumbkey of right-cluster while in QWERTY layer | Toggle | This layer contains keys that can control the Bluetooth connections of the board, and reset the board entirely |

### PCB Creation
Initially, I started with a design that I fine-tuned to match my hand from [ergogen](https://ergogen.cache.works/), a website specifically created to help improve the process of creating an ergonomic keyboard. I wrote a YAML configuration file, including PCB schematics and 3d printable bases, and exported it for use in KiCad and Fusion360. From there, I iterated over the design in KiCad, routing the hotswap sockets ergogen placed in the file to a microcontroller footprint on the main board. However, after ordering through JLCPCB, I learned there was a routing error in the drill file - a path overlapped a hotswap footprint where it should not, making a key that thought it was _always depressed_. This forced me to be more careful with my DRC before printing, though I am surprised I didn't catch this.

### Choosing a Layout
Initially, I was going to use Dvorak because it was the name that had popped up most in the academic research space on keyboard layouts. However, beyond that, in the online space, people have take what Dvorak has done and applied further optimization of keyboard layouts. As I had already decided this keyboard would use a custom layout which would require a strict learning curve anyways, I decided to go with what has been settled upon as the design with the least typing effort - that is, a layout chosen strictly for its ability to maximze rolls and alternations while reducing scissors. Each of these are specific phenomena that occur when typing, based on the most common english bigrams (sequences of 2 letters). The layout I choose, a modified [caster](https://cyanophage.github.io/#caster), is unique in that it places `e` on the thumb cluster. Most layouts avoid this simply because the thumb cluster is typically reserved for modifier and layer keys, but this is only because it is traditional.
## Building It Yourself
### Bill of Materials
| Component | Count | Details | Source | Cost | 
| -- | -- | -- | -- | -- |
| Hourglass Twins L/R PCB Pair | 1x | Gerber and Drill files can be found in this repository. Min order size through JLCPCB is 5x each half (kinda wasteful, I'm looking into a reversible design) | JCLPCB | $35 |
| nice!nanoV2 | 2x | Supports wireless capabilities and QMK | [typeractive.xyz](https://typeractive.xyz/products/nice-nano) | $50 |
| Kalih Choc LP Ambients Twilight | 32x | Regarded as one of the highest quality low profile switches with an exceptionally silent operation and light force of 35gf | [lowprokb.ca](https://lowprokb.ca/products/ambients-silent-choc-switches) | $36 |
| Kalih Choc LP Ambients Nocturnal | 6x | Used on the pinky keys with an even lighter operation force of 20gf | [lowprokb.ca](https://lowprokb.ca/products/ambients-silent-choc-switches) | $9 |
| LDSA LP Keycaps | 28x | Used for most keycaps | [lowprokb.ca](https://lowprokb.ca/collections/keycaps/products/ldsa-low-profile-blank-keycaps) | $10.50 |
| LDSA LP Homing Bar Keycaps | 2x | Used on this board's equivalent "home row," where the pointer fingers are meant to rest | [lowprokb.ca](https://lowprokb.ca/collections/keycaps/products/ldsa-low-profile-blank-keycaps) | $1 |
| LDSA LP Convex Keycaps | 8x | Used on the thumb cluster, as concave kecaps here would be hard to navigate smoothly | [lowprokb.ca](https://lowprokb.ca/collections/keycaps/products/ldsa-low-profile-blank-keycaps) | $3 |
| Kalih Choc Hotswap Sockets | 38x | Allows for future customization of keycaps if desired | [lowprokb.ca](https://lowprokb.ca/collections/keycaps/products/ldsa-low-profile-blank-keycaps) | $7 |
| SMD Diodes | 38x | Prevents ghost keys and allows matrix-scanning algorithm to function properly | [typeractive.xyz](https://typeractive.xyz/products/smd-diodes) | $3 |
| nice!view | 2x | Low power e-ink display to view layer, battery life, connected device (only 1 is neccesary on left half, but I used 2 for symmetry's sake) | [typeractive.xyz](https://typeractive.xyz/products/nice-view) | $40 |
| Reset Button | 2x | Allows to reset board to factory firmware, clearing device connections | [typeractive.xyz](https://typeractive.xyz/products/reset-button) | $1.50 |
| Power Switch | 2x | Disconnect battery from microcontroller for long term storage | [typeractive.xyz](https://typeractive.xyz/products/power-switch) | $1.50 |
| Machine Sockets + Pins | 4x12 | Used to add a swapable connection for the nice!nano to the PCB so a dead microcontroller doesn't take the device with it. Needs 4 rows of 12 sockets/pins | [typeractive.xyz](https://typeractive.xyz/products/machine-sockets-and-pins) | $13 |
| 1800 mAh LIP1359 Battery Pack | 2x | Exceptionally large battery for keyboard use, with this setup can see ~6 months of battery life with consistent usage | [amazon.ca](https://www.amazon.ca/Pickle-Power-Controller-PlayStation-Dualshock/dp/B0FYLYFLW2) | $14 |
| | | | Total Cost: | $224.50 |


## Installation
_zmk for the nice!nanoV2_

This repository hosts the necessary shields and boards for Horse-5-333's Hourglass Twins keyboard. 

Updated firmware can be found under the `Actions` tab, where each workflow contains an `firmware.zip` file containing 3 `.uf2` firmware files. Each half of the board is flashed individually by rapidly clicking the reset button until the LED on the nice!nano pulses blue. Plugging one half at this time will mount it as a mass storage device labeled `NICENANO`. Move the respective `.uf2` file (ie, `twins_left twins_view_adapter nice_view_elemental-nice_nano_v2-zmk.uf2` for the left half board) into this drive. Once file transfer is complete, the keyboard should automatically eject itself from the computer.
### The Reset Firmware
`settings_reset-nice_nano_v2-zmk.uf2` is a file in the more recent firmware packages that will clear all onboard memory on the nice!nano. This is useful to reset the bluetooth connection while testing and just factory resetting the nice!nano in case something goes wrong.
