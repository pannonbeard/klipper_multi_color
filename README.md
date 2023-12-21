# Klipper Multi-color Config
This is an attempt at making a multi color config using an arduino uno and a CNC shield.

## Items you'll need to utilize this config
- Your 3d printer running klipper
- [Arduino uno, cnc sheild and stepper drivers](https://www.amazon.com/DAOKI-Expansion-Arduino-Heatsink-Engraving/dp/B08KFYKKN4/ref=sr_1_5?crid=O6SY9OGG34GW&keywords=arduino+cnc&qid=1703170197&sprefix=arduino+c%2Caps%2C391&sr=8-5)
- up to 4x Nema 17 stepper motors
- up to 4x [extruder parts](https://www.amazon.com/Comgrow-Upgraded-Replacement-Aluminum-Extruder/dp/B07B5118T7/ref=sr_1_13?crid=2T4YEVZ3Q8SVC&keywords=ender+3+extruder&qid=1703171029&sprefix=ender+3+extrude%2Caps%2C143&sr=8-13)
- USB cable
- 12-36v power supply
- Extra PTFE tubes and connectors
- [3d printed quad splitter](https://www.printables.com/model/466735-4-to-1-bowdenptfe-tube-joinersplitter)

## Steps
- Attach Arduino to CB1/Raspberrypi
- Flash Arduino
- Upload multi_color.cfg to your klipper machine
  - Update MCU Serial path
- Setup up your Arduino and CNC sheild to your needs

## Flashing the Arduino
The hardest part of this project, other than tuning the steppers, will be flashing the arduino.
Depending on what version of debian you are running this might require you to add some specific libraries to your computer running klipper.

See this if you have any issues with the flashing procedure:
[https://github.com/Klipper3d/klipper/issues/4938#issuecomment-1094246978](https://github.com/Klipper3d/klipper/issues/4938#issuecomment-1094246978)

If you are using KIAUH to manage your klipper install you can build and flash right from inside of KIUAH

Open up KIAUH and select the following:
- [ADVANCED]
- [BUILD + FLASH]
- Select the configuration options below

### Options to select for Arduino Uno
```
Enable extra low level configuration options
MCU Architecture: Atmega AVR
Processor model: atmega328p
Processor speed: 16 MHz
Baud rate for serial port: 250000 
```

### Troubles flashing arduino??
[https://github.com/Klipper3d/klipper/issues/4938#issuecomment-1094246978](https://github.com/Klipper3d/klipper/issues/4938#issuecomment-1094246978)

## Preparing the slicer!

There are a few custom Klipper Macros to make some of this easier.
- UNLOAD_COLOR
- LOAD_COLOR
- CHANGE_COLOR
- SET_COLOR

The filament changing macros currently don't have a set of temps to allow the change so you'll need to heat your extruder before using them.

Our change gcode was put together in Orca Slicer so you will need to adjust depending on your slicer. In your filament change gcode you'll want to set it to something similar to the following:
```
; For Orca Slicer
; - Custom AMS tool T{next_extruder} -
CHANGE_COLOR NEXT_COLOR={next_extruder} DISTANCE=200
M117 Custom AMS Tool T{next_extruder}
```

## Activating Multi-Color
add ``[include 'multi_color.cfg']`` to you printer.cfg file.

## Extruders in tandum vs separate
Depending on your needs one way may benefit you more than another.

- Tandum -> Passing material to a main extruder, best for direct drive extruders
- Separate -> Passing material straight from auxillery extruders to hot end, best for bowden setups

Reguardless of your method you will want to check and update the rotation distance of the auxillery extruders you are using.

### Tandum Operation
When hooking up your multi extruder for tandum you will be passing from the PTFE extruder into your main extruder. 

### Separate Operation
This config utilizes the SYNC_EXTRUDER_MOTION klipper macro to control the extruders on and off. If you want to directly extruder from your auxillery steppers and not use the built in extruder for your machine uncomment the line:

```
# SYNC_EXTRUDER_MOTION EXTRUDER="extruder" MOTION_QUEUE=''
```

This will deactive your main extruder and let the other extruders take main control.

You'll then need to go from your PTFE Joiner straight into the hotend.

