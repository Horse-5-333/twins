# Firmware for The Twins Keyboard
_zmk for the nice!nanoV2_
This repository hosts the necessary shields and boards for Horse-5-333's Hourglass Twins keyboard. 
## Installation
Updated firmware can be found under the `Actions` tab, where each workflow contains an `firmware.zip` file containing 3 `.uf2` firmware files. Each half of the board is flashed individually by rapidly clicking the reset button until the LED on the nice!nano pulses blue. Plugging one half at this time will mount it as a mass storage device labeled `NICENANO`. Move the respective `.uf2` file (ie, `twins_left twins_view_adapter nice_view_elemental-nice_nano_v2-zmk.uf2` for the left half board) into this drive. Once file transfer is complete, the keyboard should automatically eject itself from the computer.
### The Reset Firmware
`settings_reset-nice_nano_v2-zmk.uf2` is a file in the more recent firmware packages that will clear all onboard memory on the nice!nano. This is useful to reset the bluetooth connection while testing and just factory resetting the nice!nano in case something goes wrong.
