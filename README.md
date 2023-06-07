# USG-FIRM-WRITER
Hardware and software to manage DS lite (USG) firmware. Using this requires making a USG-FIRM-WRITER cart to read/write the WiFi board (this holds the firmware) through the cartridge port, as well as a modded 2/3DS to run the script (optional). Assembly details are below.

This project is not very practical for most and I only recommend using it if you find yourself having 170+ WiFi boards... 

## Table of Contents
1. [How the cart works](#how-the-cart-works)
2. [Assembling the cart](#assembling-the-cart)
3. [Running the script](#running-the-script)
4. [Credits](#credits)

## How the cart works
The DS lite WiFi board stores firmware on the same exact flash chip as the save chip in most DS cartridges, meaning that both chips are read and written to in the same way. If you remove the save chip from the cart and wire the WiFi board along the same lines, you can redirect the signals to the firmware chip and "trick" the DS into treating it as just another save file. 

Normal methods might include hotswapping WiFi boards on a DS lite motherboard (risk of shorting), or holding SL1 shut on writing (immediate brick if you let go). This replaces those dangerous methods with a safer, faster, and more powerful<b>*</b> option that can be used on any DS console.

<sup><b>*</b>currently the only flashing tools that exist will permanently break wireless without proper preperation, do not fully support 512kb firmwares, do not transfer user data, and (mostly) aren't maintained anymore</sup>

## Assembling the cart
You will need basic soldering supplies as well as the following parts:
- DS cartridge with a board ID of `C03-10` or `Y10-01`
- [Molex 52991-0308](https://mou.sr/42sjkJz) socket
- Molex socket breakout board. See gerber files for a premade board one [here.]() (can to be sent to a PCB manufacturer like [PCBWay](https://www.pcbway.com/))

Steps:
1. Remove the shell from the cartridge
2. Desolder the save chip (the smaller of the two, labelled as `U2`)
3. Solder the Molex socket to the breakout board
4. Solder wires between the cartridge and breakout board along the contact points listed below (first value is cart, second is breakout board/Molex socket):
    - If using the gerber files above: `1-1`, `2-2`, `3-3`, `4-4`, `5-5`, `6-6`, `7-7`, `8-8`
    - If using your own board, refer to the chart below and connect `1-11`, `2-13`, `3-17`, `4-5`, `5-7`, `6-29`, `7-27`, `8-9`

Having trouble finding which pin is what number on the cartridge? Refer to this chart, and note that the ink will have the same semicircle "cut out" around the U2/save chip pads. Match the orientation of that on the board with the chart.
![image](https://randommeaninglesscharacters.com/assets/dsi/blog/UTL-FIRM-WRITER.jpg)

After having connected the wires, you should be good. Plug a WiFi board into the Molex socket, plug the cartridge into any DS console, then try dumping the save. Check any outputted `.sav` file in a hex editor to make sure they're proper firmware dumps.

Then, test the board by editing the `.sav` file (could be replacing it with a new firmware or patterns) and restoring it. Dump again to make sure the data was correctly written.

## Running the script
CFW and GodMode9 must already be installed, I will not go over this here.

1. Download the [script](https://github.com/IanSkinner1982/USG-FIRM-WRITER/blob/main/Script.gm9) from this repository
2. Copy the downloaded script to your 3DS SD card at `SD:/gm9/scripts/`
3. Open GodMode9 on your 3DS
4. Press the `home` button, then navigate to `Scripts...` on the opened popup
5. Select the downloaded script and press the `A` button
6. Have fun running it and doing whatever 

## Credits
- `Haifisch` for the breakout board
- [This blog](http://imaginglabo.web.fc2.com/DSL-Fw.htm) for explaining accessing WiFi boards via save chip lines
