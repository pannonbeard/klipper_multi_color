# Klipper Multi-color Configs for Arduino Uno and Rpi Pico
While exploring options of adding extra I/O, I found that using a usb with an arduino and cnc sheild I had laying around could make multicolor an option. Here are my findings with both Arduino over usb and a Rpi Pico with a canbus connection.

## Why no arduino uno canbus??
Right now klipper only supports [CAN on stm32, SAME5x, and rp2040 chips](https://www.klipper3d.org/CANBUS.html#device-hardware). Arduino uno doesn't quite make the cut in this case.

## Items you'll need to utilize Arduino config
- Your 3d printer running klipper
- [Arduino uno, cnc sheild and stepper drivers](https://www.amazon.com/DAOKI-Expansion-Arduino-Heatsink-Engraving/dp/B08KFYKKN4/ref=sr_1_5?crid=O6SY9OGG34GW&keywords=arduino+cnc&qid=1703170197&sprefix=arduino+c%2Caps%2C391&sr=8-5)
- up to 4x Nema 17 stepper motors
- up to 4x [extruder parts](https://www.amazon.com/Comgrow-Upgraded-Replacement-Aluminum-Extruder/dp/B07B5118T7/ref=sr_1_13?crid=2T4YEVZ3Q8SVC&keywords=ender+3+extruder&qid=1703171029&sprefix=ender+3+extrude%2Caps%2C143&sr=8-13)
- USB cable
- 12-24v power supply
- Extra PTFE tubes and connectors
- [3d printed quad splitter](https://www.printables.com/model/466735-4-to-1-bowdenptfe-tube-joinersplitter)
- A 2 to 4 color holder or stand

## Arduino Steps
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

## Rpi Pico Steps w/ canbus
This does require a few extra components to get it to work. If you wanted to use usb instead of canbus, you can flash it with your preffered usb settings for the pico.

- Create Config for Rpi Pico
- Flash Pico
- Solder together board to connect the pico to the cnc shield
- Upload multi_color_rpi_pico.cfg to your klipper machine
  - Update MCU Serial path
- Setup up your Arduino and CNC sheild to your needs

Extras needed:
- [Rpi Pico](https://www.amazon.com/Raspberry-Development-Dual-core-Processor-Integrated/dp/B0CPMBRVDX/ref=sr_1_4?crid=L1CHGUTTQ84H&dib=eyJ2IjoiMSJ9._ppkHtY7vs-4LrTJ-McqCu1TUecr6CsdDR6efMbrA8WPjMqv9WjVU6DcHHFAzA5puIvi6Si_lsSmVZTKbH91SAuwXFPLK2wCbo_40BANJ8TsDWlWbMPMhQR6_oRgyadTB8gKAw-e5-GcizpbW09U6ldzaYstuV6lxaHbGvRfFWJIB5HpFneT_VIBhCnQ0864Gs3cty2wE8SEwzn_X57HyE6gyzNJle9aQCBkhNKRd8w.l_6Y5UI3ovRzEVuJOWbXD5v7WxOUXl5LFb3c2sofQSU&dib_tag=se&keywords=pi+pico&qid=1741572097&sprefix=pi+pico%2Caps%2C144&sr=8-4) (instead of the arduino of course)
- [5v regulator](https://www.amazon.com/Regulator-Step-Down-Converter-MP1584EN-Aircraft/dp/B0DSZKQGBZ/ref=sr_1_2_sspa?crid=13KWI139KTW4K&dib=eyJ2IjoiMSJ9.KKh06qsL4egEaC49ZvfCUnga4qWmuIudwgSt4MXuAf12uSAPdpct8lo2VMLGpUbK6p1CjCXBeHOWUCfLQX9hERO9wD3RmOfhcZn2dy5s7Psb0_rcjMIkL6HwW0OCTkTqNIbDV3MhwZvI2bo5ZT2bwhT9zvI0A9tTjD29A3GbGZJB9mMI3Qb5y0AEl1F52SswXahNUaGy_L0oao6GT7uzgNaa7f_FaFL4IZAdBYaXzpUgSaeuV4qfV-H3igSJ__IgHNIAwBLzGRQqogCqO01R69iReVpl2hTpDFybD7RFTmg.GMzQw9K2ANzKsYbHWC9f5Fo5A_vTHLjkaR3XVUfGoFU&dib_tag=se&keywords=arduino+5v+regulator&qid=1741571818&sprefix=arduino+5v+regulato%2Caps%2C170&sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1)
- [Canbus Transiever](https://www.amazon.com/Comimark-Transceiver-TJA1050-Controller-Schnittstelle/dp/B07W4VZ2F2/ref=sr_1_6?crid=3UUQ0WMAKBQ9T&dib=eyJ2IjoiMSJ9.NNL58DY5rs0tgrb226Z743zWN8BDbmSIM8wmN1WWJ2YklFU70S0qRFwhFjIpNHzKXr7jLPG3msQJ1cjmFi8bQqkKDzD4uvJp2ktCt7moMfijR2BuZKqyshqfsyDogVMdHmk8yUddm-i_5ay8QQIGfwSj4XR20p2_1yf3kVp387Du9V27y2y99Nx7jHHmFGdG-rDUqfVvL9iUiaPTmm4g-mp2dv9WKIQm4HDBtRL6vbU.haqqTQ4DeLRvuclpCep427jMVSTh_vaFISucwu1C2Po&dib_tag=se&keywords=arduino+canbus&qid=1741571775&sprefix=arduino+canbus%2Caps%2C122&sr=8-6)
- If no can network [a canbus to usb connector](https://www.amazon.com/FYSETC-STM32F072-Interface-Candlelight-Firmware-Pack/dp/B0BPY5HY6C/ref=sr_1_10?crid=21PWTQ6N64RAU&dib=eyJ2IjoiMSJ9.G7yb_kcxYXUZF5oXmMs5a76vK5ESAj9yFeHi24UY5TlHmDgMu44lJKIgRkhbou0ivgAuUe-9u_2Q0wTiJLtJOgn2czgo6Q2nQxLGfEvZ6GsVcQ1ayGmIQsWsPj8TTkvMIX36N__weTc3NrZwT0-aipwJgnLjzjWLLH_9kH0dew7c88pe9wUlNNvTCLkY6hoLCBk5s1sDY6g1JekDeNZ3DHcnspWpboJjucpi18M4eKQ.QP0HqxScm5Gspfbn9y99oVRyHdHoaIzn15dp9q7zMGE&dib_tag=se&keywords=usb+to+canbus&qid=1741572598&sprefix=usb+to+canbus%2Caps%2C135&sr=8-10)
- Soldering iron
- Solderable Project board and Screw Terminals (I got these in a [kit](https://www.amazon.com/Sunxeke-Soldering-Electronic-Compatible-Connector/dp/B0BWCFH57N/ref=sr_1_16?crid=2GVC1KBEVDEVE&dib=eyJ2IjoiMSJ9.JQS93JxT9fTg_Qec5prcl7al7vOkyxKy5UiUVLHgq8xwurRgQW98DkB6WHH6_8qHGtafjirL_wfynDdqTwX6Jf4lvuMTn1Dx6AhqZX8AwW0Dkg0eO1SBgi-23lJEM_vODruIG6sPVAVU8Y3V4CK15wrOwOmY9MAbvDXe5w2zfsiIMr9cwaW-Y6IhUcYOFPh5-3rZ6BLdPPwz0N2wU9GyUj9fg-i_cbYMieUXsXykGI8ZqmjYcMZx8VNgsC3IVOshVIT6LcdJ56dgunQyhJw0m0PELgJf0TmgoWfn8Kwe-5iJQ5jKnsQgLubhVQxWSHEMWblKRDbavoJAVUwYCThXOykll9kZf-CLcyHggB_W_4Cb8GBzLxPO39aODuISS_aA5Ey5USL29j7OiBzaC7sK7EEM7XKEq-ajynHZ-aunMbUViCWD07jPqYtGOc_xdxKh.PWyL7fVF9fudB6r4W5Y8kPY1CIk4oalaPABr0BZkRzo&dib_tag=se&keywords=soldering%2Bproject%2Bboard&qid=1741572021&sprefix=soldering%2Bproject%2Bboard%2Caps%2C126&sr=8-16&th=1))
- Hookup wire (multi colors to help tell things apart)

This does require some soldering skills and tools so... prepare yourself.

### Flash Options for Pi Pico w/ canbus
You can either setup the flashing file for the pico by either through the klipper folder or KIAUH, here we will do the klipper folder.
Enter `cd klipper && make menuconfig`

```
[*] Enable extra low-level configuration options
Micro-controller Architecture (Raspberry Pi RP2040/RP235x)  --->
    Processor model (rp2040)  --->
    Bootloader offset (No bootloader)  --->
    Flash chip (GENERIC_03H with CLKDIV 4)  --->
    Communication Interface (CAN bus)  --->
(4) CAN RX gpio number
(5) CAN TX gpio number
(500000) CAN bus speed
```

### Copy file to klipper config folder
From the klipper out folder you will need the `klipper.uf2` file. You just need to download it.

### Flash pico
On your main pc, not the comp for the printer, hook up the pico while holding the "boot" button down.
It should attach the pico as a storage device. Transfer the Klipper.uf2 file into that storage device. It will reboot and flash the pico.
It is now flashed with klipper.

## Interfacing the Pico and the CNC sheild
This will require some soldering equiptment, project circuit boards, and other items to attach the pi and the shield together.
In my current configuration I have attached the following:
```
PICO GPIO6 -> CNC Enable pin
PICO GPIO7 -> Y DIR
PICO GPIO8 -> X DIR
PICO GPIO9 -> Y Steps
PICO GPIO10 -> X Steps
```
You can attach these pins in any way you like there are so many options on the pi pico.

### Note about powering the pico, canbus transiever and the drivers
One thing that caught me up for a while was that there is a 5v line that would normally be fed from the arduino that is plugged in over usb to the cnc board. This 5v connection is essencial for the drivers to work.
You should connect the `+/-` of the 5v regulator to `VSYS / GND` on the pico, the `VCC / GND` on the canbus transiever, and the `5v line` of the CNC Sheild.

### Note about wiring the Canbus Transiever and Pico together
For what ever pins you set in the menuconfig as your RX/TX pins, be sure to hook them to the opposite pins on the Transiever board so RX -> TX and TX -> RX. 

## Setup can network
On your klipper device enter `sudo nano /etc/network/interfaces.d/can0` and set the contents of the file to the following: 
```
allow-hotplug can0
iface can0 can static
    bitrate 500000
    up ifconfig $IFACE txqueuelen 1024
```
You really need your bitrate of this file to match the CAN bus speed you set in the pico menuconfig.

### Checking if can connection is working
Once you've updated your can file you can do two things to check that can is working. Connect your USB can device first.
Enter: `sudo ifconfig can0`
You should see something that indicates that the can network is communicating with your usb device.
Something like:
```
can0: flags=193<UP,RUNNING,NOARP>  mtu 16
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen 1024  (UNSPEC)
        RX packets 17302  bytes 131255 (128.1 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 7790  bytes 46521 (45.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Getting your UUID
With your can usb device wired into your can to usb device enter `~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0`.
If you have everything connected correctly you should see a UUID appear. If not then double check that your have your CanH and CanL's connected to the correct parts of the can to usb board. 
If the can to usb board has screw terminals this would be just switching them and running the above command again.

There might be a resistor that needs to be either soldered or plugged into the board for the can to usb to work here. Also double check if your can to usb board needs this or already has it in place.

# Preparing the slicer!

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

#### Note:
In Orca turn off ramming when running separate. Orca slicer does set ramming properties with a PRESSURE_ADVANCE setting for klipper machines that I haven't figured out how to get rid of. If you removed the main extruder from the motion queue this does throw an error and will stop your print dead in it tracks. WHen the main extruder is removed it has no idea what extruder to apply the pressure advance to.

# Want to contribute?!
Happy to have any help! I am not yet the best will all of the amazing things you can do with klipper, but any other ideas of things we can add or improve with this are greatly appriciated!

Open a issue or possibly a pull request and we can have some fun troubleshooting!

