# Espruino on NodeMCU ESP8266-12E

1. Follow the setup procedure from the [main readme](../README.md).

2. Download the firmware files from [Espruino](https://www.espruino.com/binaries/espruino_2v03_esp8266_4mb/):
	- NOTE: The listed files are for the 4MB board. If you have a 512kb board you will need to find the appropriate files [here](https://www.espruino.com/binaries/espruino_2v03_esp8266/).
	- `wget https://www.espruino.com/binaries/espruino_2v03_esp8266/blank.bin`
	- `wget https://www.espruino.com/binaries/espruino_2v03_esp8266/boot_v1.6.bin`
	- `wget https://www.espruino.com/binaries/espruino_2v03_esp8266/esp_init_data_default.bin`
	- `wget https://www.espruino.com/binaries/espruino_2v03_esp8266/espruino_esp8266_user1.bin`
	- **Or, unzip from this repo and move the files to root:** 

		```
		unzip espruino-2v03.zip && mv espruino-2v03/* . && rm -rf espruino-2v03 && rm -rf __MACOSX/
		```

3. Flash the firmware to the board.
		```
		esptool.py --baud 115200 --port /dev/tty.SLAB_USBtoUART write_flash -fs 4MB -ff 80m --flash_mode dio 0x0000 boot_v1.6.bin 0x1000 espruino_esp8266_user1.bin 0x3FC000 esp_init_data_default.bin 0x3FE000 blank.bin
		```
	
	- NOTE: If you are on a 512kb board your command will need to be different. Take a look [here](https://github.com/espruino/Espruino/blob/master/targets/esp8266/README_flash.txt).
	- I can't confirm this, but it will probably be something along these lines:

		```
		esptool.py --port /dev/tty.SLAB_USBtoUART --baud 115200 write_flash --flash_freq 40m --flash_mode dio --flash_size 4m 0x0000 boot_v1.6.bin 0x1000 espruino_esp8266_user1.bin 0x7C000 esp_init_data_default.bin 0x7E000 blank.bin
		```

	- You should see a confirmation that the board was successfully flashed. It will look something like this:
	
		```
		esptool.py v2.6
		Serial port /dev/tty.SLAB_USBtoUART
		Connecting........_
		Detecting chip type... ESP8266
		Chip is ESP8266EX
		Features: WiFi
		MAC: 84:0d:8e:8d:44:95
		Uploading stub...
		Running stub...
		Stub running...
		Configuring flash size...
		Flash params set to 0x024f
		Compressed 3856 bytes to 2763...
		Wrote 3856 bytes (2763 compressed) at 0x00000000 in 0.2 seconds (effective 124.3 kbit/s)...
		Hash of data verified.
		Compressed 520356 bytes to 343690...
		Wrote 520356 bytes (343690 compressed) at 0x00001000 in 30.4 seconds (effective 137.1 kbit/s)...
		Hash of data verified.
		Compressed 128 bytes to 75...
		Wrote 128 bytes (75 compressed) at 0x003fc000 in 0.0 seconds (effective 93.3 kbit/s)...
		Hash of data verified.
		Compressed 4096 bytes to 26...
		Wrote 4096 bytes (26 compressed) at 0x003fe000 in 0.0 seconds (effective 4703.9 kbit/s)...
		Hash of data verified.

		Leaving...
		Hard resetting via RTS pin...
		```
	
4. You're almost ready to open the board in the Espruino editor.
	- Before connecting your board to the editor, open up the Espruino Web IDE.
	- Go to `Settings > Communications` and set the `Baud Rate` to `115200`.
	- Connect your board to the IDE and you should be good to go. You can write code in the editor, flash it to the board, and interact with it as you would an Espruino board (with some caveats).
	- NOTE: If you go back to using a normal Espruino board you will need to return the `Baud Rate` to `9600`.


## Resources

[EspruinoESP8266](http://www.espruino.com/EspruinoESP8266)

[Espruino Binaries](http://www.espruino.com/Download)

[Flashing ESP8266 with Espruino](http://www.espruino.com/ESP8266_Flashing)

[Flashing with esptool.py](https://github.com/espruino/Espruino/blob/master/targets/esp8266/README_flash.txt)

[Video detailing the process](https://www.youtube.com/watch?v=j9xwgeE9u8E)
