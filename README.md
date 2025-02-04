# RC2040

Z80 emulation of RC2014 using the RP2040 processor.

Initial aim was to get the [EtchedPixels](https://github.com/EtchedPixels) Linux based Z80 emulation including an SD Card based IDE running on a Pi Pico as a standalone.
I have ripped out much of EtchedPixels's great work, to which I'm truly sorry, but I was only interested in the Z80 emulation, and I needed to get it to fit in an RP2040

## PCB
A PCB and a full kit of parts is available here https://extkits.co.uk/product/rc2040/ for this project from Extreme Kits http://www.extkits.co.uk 

![20220514_162232](https://user-images.githubusercontent.com/102665314/168440015-87bc3225-e370-4dfc-a1a9-9be01d625213.jpg)

## Documentation

A lot more detail is available at https://www.extremeelectronics.co.uk/the-rc2040/

### Compiling

I use a RPI so...
Install Raspberry Pi SDK
Clone this RC2040 git into a subdirectory under the pico one then,

```shell
  cd pico/RC2040
  cp ../pico-sdk/external/pico_sdk_import.cmake .
  mkdir build
  cd build
  cmake ..
  make
 ```

For more details look at [Compiling.md](Compiling.md)

## SD card connection to the Pico

Details are in the Circuit diagram folder. Switches and buttons are not required. Just an SD card that can be easily attached using an old SD adapter. (diagram for this in the Circuit diagram folder)

## Serial connection details

UART 115200 N81 3ms/char delay - 3ms/line delay (1ms /3ms if overclocked at 250000)

USB  115200 N81 3ms/char delay - 3ms/line delay (1ms /3ms if overclocked at 250000)

## 8 Bit output

- port 0 mapped to 8 GPIO pins see circuit diagram
- out(0,val) will make them outputs outputting val
- in(0) will make them inputs (with pullups) returning the port state value

### ROM images

SD card images (a "get you started" is available in the [SD Card Contents] sub folder) other ROM images can be found:

- Z80 Base ROM images - https://github.com/RC2014Z80/RC2014/tree/master/ROMs/Factory
- Z80/180 Small Computer Monitor - https://smallcomputercentral.wordpress.com/small-computer-monitor/
- Z80/180 ROMWBW - https://github.com/wwarthen/RomWBW/releases
- Etched Pixels non Z80/180 cards - https://github.com/EtchedPixels/RC2014-ROM

### CP/M Disk Images (for non ROMWBW systems)

- https://github.com/RC2014Z80/RC2014/tree/master/CPM

### CPM manual

- http://www.cpm.z80.de/manuals/archive/cpm22htm/index.htm

### Real hardware Boards

- RC2014 - RFC2795 Ltd: https://z80kits.com
- Small Computer Central: https://www.tindie.com/stores/tindiescx/
- Etched Pixels: https://hackaday.io/projects/hacker/425483
- TMS9918A card: https://www.tindie.com/stores/mfkamprath/

### Sound

Sound is output on GPIO 14/15. GPIO 15 is inverted WRT GPIO 14 so you can connect a high impedance a speaker directly across these two IO pins, a piezo speaker is ideal. A much better sound quality (and a much louder sound) can be heard using a low pass filter and an amplifier. Amplified external PC speakers work well.

## Beep

A background frequency generator can be accessed via Port 0x31
There are 126 notes defined 1-127 (from MIDI notes) sending either 0 or >128 will silence the currently playing note.

For examples, look in the basic examples folder

## SPO256-al2

An Emulation of the SPO256-al2 chip can be accessed on port 0x30
Sending a value of 0-63 will play one of the predefined allophones that was contained in the original chip.
reading the port will give you a non-zero value if the "chip" is still playing.

See my SPO256-AL2 Git folder https://github.com/ExtremeElectronics/spo256-al2 for more information.
Especially the Additional folder https://github.com/ExtremeElectronics/spo256-al2/tree/main/Additional

The Allophone (decimal) numbers can be sourced from "Allophone DataSheet Addendum.txt" and the full data sheet is also in this directory which should give you an idea how to use it.

For examples, look in the basic examples folder

## Progress

Now looking at documenting it and adding "useful" stuff to the build

Huge thanks goes to EtchedPixels, Grant Searle, Mitch Lalovic and Spencer Owen(Rc2014) for collating, modifying and allowing us to play with their software. and https://github.com/guidol70 for help with the img/cf file formats and diskdefs
