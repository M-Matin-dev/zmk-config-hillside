Getting Started
This document will guide you through installing your nice!nano and flashing. After following this document, you can move on to the Wireless Firmware page to pick out your software.

Before you start#
Before you install your nice!nano please note these tips/warnings:

When soldering the nice!nano, avoid using high iron temperatures, as you could damage the main nRF52840 chip. A temperature around 270°C-300°C should be hot enough. The higher the temperature, the more likely you are to damage the board.

Do not install sockets or post headers to the B+ or B- pins (top pin on each side)
If you need to use these pins with your PCB, RAW and GND are the respective equivalents to B+ and B-
The square post headers that come with the nice!nano cannot be used with the machine sockets
Use Mill-Max pin legs or diode legs and follow the directions in installing your nice!nano
Only use 3.7V rechargeable lithium batteries with the nice!nano. Connecting non-rechargeable batteries is unsafe
If you choose to solder your battery, use the B+ and B- pins. B+ is for the positive, red wire, and the B- pin is for the negative, black wire. Minimize how long you are holding the soldering iron to the battery. High amounts of heat are dangerous to connect the battery to.
If you are using a JST connector on the PCB to connect the battery, double or even quadruple check the polarity of the JST connector before plugging it in. Some batteries come with positive on the first pin and some come with negative on the first pin.
Installing your nice!nano#
Installing your nice!nano is almost the same as any other Pro Micro like board. The only difference is related to ignore the B+ and B- pins when adding sockets or headers and the battery. It's highly recommended to get your firmware on and functioning before adding the battery.

If you aren't socketing, you probably want to get the firmware up and running before you even attach the square post headers. You'll want to install the firmware, confirm everything is working, and install your square post headers and battery.

If you are socketing, you can socket your nice!nano, install the firmware, confirm everything is working, and finally add the battery.

Socketing the nice!nano#
Socketing the nice!nano is extremely recommended. It offers ease of access to the battery, helps you if you need to debug your keyboard, and lets you move the board to another keyboard if ever needed.

For a great guide with pictures check out 40percentclub's guide.

Socketing steps:

First install the socket into the PCB trying to keep it as straight as possible.
Once the sockets are in, place tape over the top of each side.
Poke holes where each socket hole is into the tape
Place down the nice!nano (to assure alignment, make sure the B+ and B- pins are not being put into the socket)
Put MillMax pin legs (or diode legs) into each hole and push all the way down
Solder the legs to the nice!nano (this is where the tape helps, solder wont seep down into the socket and fuse the socket and legs)
Take the nice!nano out by using a pry tool of some sort. Slowly pry back and forth on all sides.
Take away the tape and put the nice!nano back in.
Done!
Flashing, Firmware, and Bootloaders#
One of the great things about the nice!nano is how easy it is to flash the device. To jump into the bootloader all you need to do is double tap reset. You can do this by either double tapping your reset button on your keyboard, or you can double tap RST and GND pins on the nice!nano quickly with tweezers.

Once you are into the bootloader, connect your nice!nano via USB to your computer if you haven't already. Your nice!nano should now show up in your OS as a USB storage device named "NICENANO".

Flashing is now as easy as copying a .uf2 firmware file to the storage device. You can do this by copying in the terminal, dragging and dropping it in your file explorer, or however else you copy files to a storage device in your OS.

Now you may be wondering how to get one of these mystical .uf2 files. You get them by building one of the firmwares available. Checkout the Wireless Firmware page to get information on how to configure and build a few different types of firmwares along with some recommendations.

The bootloader the nice!nano uses is the Adafruit nRF52 Bootloader. You can read more about its features, updating the bootloader, and using DFU to flash firmware on its GitHub.

-----

Frequently Asked Questions
Will the nice!nano work on my keyboard?#
Almost every Pro Micro based keyboard should work with the nice!nano. If you want to use the nice!nano on an existing keyboard, it will be much more complicated and will require "hijacking" the existing matrix.

The nice!nano will NOT work with the Gherkin or Helix unless you leave the RAW pin disconnected from the board.

How is the nice!nano powered/how do the split boards power each other?#
They don't charge or power each other. Each side has an individual Li-Po battery connected to it via 2 extra pins at the top of the board (called B+ and B-).

How do you charge the nice!nano?#
The nice!nano has a Li-Po charger built in that uses the USB-C port to charge the Li-Po at a rate of 100mA.

How long does the nice!nano last on battery?#
This is highly dependent on the battery size and features of the keyboard. The power profiler from ZMK offers a good estimate of the battery life you can expect.

Does the nice!nano work over USB?#
Yes!

Do you still need a TRRS jack?#
No, there's a connection via BLE between the two boards. The central half reports back the keystrokes of both the central (usually left) and peripheral (usually right) sides.

QMK firmware support?#
This is complicated. Nordic's nRF52 line has some licensing issues with its SDK making it not possible to be upstreamed to the main QMK repo. Instead, we rely on other firmwares like ZMK or BlueMicro that offer a great deal of functionality with full legality and wireless focus.

Can I get more information on nRF52840 hardware?#
Joric's nRFmicro wiki is an amazing resource to get some basic and advanced information on the nRF52 line in terms of keyboards: https://github.com/joric/nrfmicro/wiki

How is this different from the nRFMicro or BlueMicro?#
The nRFmicro is extremely similar to the nice!nano. The main difference is depending on the version of the nRFMicro, the power system would be slightly different from the nice!nano. From a usability standpoint, very little is different. The nice!nano exposes more pins and is thinner than older versions of the nRFMicro. The biggest difference is that the nice!nano is prebuilt and has a large user base, which therefore has a bigger support community. The BlueMicro is basically the same story except for the nRF52832 versions don't support USB.

-----

Troubleshooting
Troubleshooting your nice!nano often falls on to the firmware of choice, but a few directly hardware related items can be addressed.

My nice!nano seems to be acting up and I want to re-flash the bootloader#
I can still get into the existing bootloader over USB#
In this case you can most likely re-flash the bootloader using adafruit-nrfutil. Here are the steps you'll want to follow:

Follow the installation section here. Most likely you'll just need to run pip3 install --user adafruit-nrfutil.
Download the DFU pkg of the nice!nano bootloader.
Connect your nice!nano and put it into the bootloader using a double-tap reset.
Run the following command in your terminal:
adafruit-nrfutil --verbose dfu serial --package nice_nano_bootloader-0.6.0_s140_6.1.1.zip -p SERIALPORT -b 115200 --singlebank --touch 1200
However, replace SERIALPORT with your respective serial port name on your OS.

On Windows it will be in the format of COM8, but the number 8 will depend on what it is in your device manager under serial.
On MacOS and Linux it will look something like /dev/ttyS0, but you'll of course need to double check the exact path name.
After this runs, you should have your bootloader all re-flashed and fresh.

I can't get into the bootloader at all anymore#
If you can't get into the bootloader anymore, this will mean you'll need a device programmer. You can select one of the two below and use the steps listed.

J-Link (~$30)#
Plug in your nice!nano over USB
Connect these 4 pins to the nice!nano (use the pinout as reference)
VCC/VTref will connect to the VCC pin on the nice!nano
GND will connect to any of the GND pins on the nice!nano
SWDIO will connect to the SWD pin on the back of the nice!nano
SWCLK will connect to the SWC pin on the back of the nice!nano
Download the bootloader hex
Download nrfjprog
Run this command in your terminal
nrfjprog -f NRF52 --program nice_nano_bootloader-0.6.0_s140_6.1.1.hex --chiperase
ST-Link v2 (~$4)#
Plug in your nice!nano over USB
Connect these 2 pins to the nice!nano (use the pinout as reference)
SWDIO will connect to the SWD pin on the back of the nice!nano
SWCLK will connect to the SWC pin on the back of the nice!nano
Download the bootloader hex
Download openocd
Run this command in your terminal
openocd -f interface/stlink.cfg -f target/nrf52.cfg -c "gdb_flash_program enable" -c "gdb_breakpoint_override hard" -c "init" -c "reset halt" -c "flash write_image erase ./nice_nano_bootloader-0.6.0_s140_6.1.1.hex"
My nice!nano won't connect to my host device over BLE#
Unfortunately there's likely not much you can do from a hardware perspective if you're running into this. This will mostly likely come down to two factors: the firmware you're using and how nicely the host BLE stack works with said firmware.

Because there's no simple way for me to offer advice on how to fix this, I would instead ask you to reach out to the respective firmware communities to ask for assistance. In general though, I would first test to see if you can connect to your phone over BLE. This will show whether it's a hardware issue or not. In my experience it's never truly been the nice!nano that has hardware issues, so continued work on the firmware side and OS stack side need to occur.

---

nice!nano v2
Pinout#
Pinout v1

Schematic#
Schematic v1

nice!nano v1
Pinout#
Pinout v1

To further clarify:#
P0.04 (AIN2) is used to read the voltage of the battery via ADC. It can't be used for any other function.
P0.13 on VCC shuts off the power to VCC when you set it to high
This saves on battery immensely for LEDs of all kinds that eat power even when off
Schematic#
Schematic v1
___

Getting Started
Installing your nice!view#
Using an existing OLED compatible shield#
Cut off one of the positions of both the socket and header
Solder the left over 4 pin socket to your shield
Solder the left over 4 pin header to your nice!view's left 4 pins (not the CS pin!)
Create a bodge wire from the CS pin to the Arduino Digital 1 (D1) Pro Micro pin (P0.06/006 on the nice!nano)
If the D1 pin is unavailable, you'll need to override the cs-gpios on the adapter or define your own &nice_view_spi bus without the nice_view_adapter.
Insert the header into the socket
Using a nice!view native compatible shield#
Solder the 5 pin socket to your shield
Solder the 5 pin header to the nice!view
Insert the header into the socket
Protection Film#
The display of the nice!view comes with a protection film installed to protect the display before usage. You may remove the film after installation or leave it on if you prefer.

Using with ZMK#
After successfully installing your nice!view, all that should be required is to build your board with the nice_view shield and possibly the nice_view_adapter if you're using a non-native shield.

ZMK Config Repo#
With a ZMK config repo, edit the build.yaml file to have nice_view added to the end of each shield string. If you're using an OLED compatible shield, you'll also need to add nice_view_adapter to the list of shields first.

Native example:

include:
- board: nice_nano_v2
- shield: some_native_shield
+ shield: some_native_shield nice_view
Non-native example:

include:
- board: nice_nano_v2
- shield: lily58_left
+ shield: lily58_left nice_view_adapter nice_view
- board: nice_nano_v2
- shield: lily58_right
+ shield: lily58_right nice_view_adapter nice_view
Manual ZMK build#
When building manually, all that needs to be done is adding nice_view to the shield build string. If you're using an non-native but OLED compatible shield, you'll also need to add nice_view_adapter to the list of shields first.

Native example:

- west build -p -b nice_nano_v2 -- -DSHIELD="some_native_shield"
+ west build -p -b nice_nano_v2 -- -DSHIELD="some_native_shield nice_view"
Non-native shield:

- west build -p -b nice_nano_v2 -- -DSHIELD="lily58_left"
+ west build -p -b nice_nano_v2 -- -DSHIELD="lily58_left nice_view_adapter nice_view"
---

Pinout#
Pinout

Dimensions#
Dimensions

Schematic#
Schematic

Default pins#
The nice!nano can be configured to use almost any pins for the nice!view display, and you would then need to configure these in the firmware of your choice. To design a shield that uses the default pins and the easy to use nice!view adapter in ZMK, use these pins: CS = D1 / P0.06 SCL = D2 / 0.17 MOSI = D3 / P0.20
---
