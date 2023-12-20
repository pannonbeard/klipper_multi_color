# Klipper Multi-color Config
This is an attempt at making a multi color config using an arduino uno and a CNC shield.

## Items you'll need to utilize this config
- Your 3d printer running klipper
- Arduino uno
- Uno CNC Sheild
- up to 4x stepper drivers
- up to 4x Nema 17 stepper motors
- USB cable
- 12-36v power supply

## Steps
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

