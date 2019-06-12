# Espruino on ESP8266

1. Download [USB to UART Bridge VCP Driver](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers) and install the driver.
	- [Direct download for MAC](https://www.silabs.com/documents/public/software/Mac_OSX_VCP_Driver.zip)
	- `wget https://www.silabs.com/documents/public/software/Mac_OSX_VCP_Driver.zip`
	- **Or use the included:** `unzip Mac_OSX_VCP_Driver.zip`
	- Once unzipped, `open Mac_OSX_VCP_Driver/SiLabsUSBDriverDisk.dmg` 
	
2. Plug in your board and verify it's COM Address.
	- `sudo ls /dev/tty.*`
	- You will need to enter your admin password
	- You should see `/dev/tty.SLAB_USBtoUART` listed. If not, verify the driver was installed correctly. You may need to grant privelages to it in security settings.

3. Download the Python tools for flashing the firmware to the board.
	- Create a virtualenv to stay clean: `mkvirtualenv esp8266-espruino`
	- Download esptool: `pip install esptool`
	- Download pyserial: `pip install pyserial`
	- **Alternatively, using this repo:** `pip install -r requirements.txt`

4. Download the firmware files from [Espruino](https://www.espruino.com/binaries/espruino_2v03_esp8266_4mb/):
	- NOTE: The listed files are for the 4MB board. If you have a 512kb board you will need to find the appropriate files [here](https://www.espruino.com/binaries/espruino_2v03_esp8266/).
	- `wget https://www.espruino.com/binaries/espruino_2v03_esp8266/blank.bin`
	- `wget https://www.espruino.com/binaries/espruino_2v03_esp8266/boot_v1.6.bin`
	- `wget https://www.espruino.com/binaries/espruino_2v03_esp8266/esp_init_data_default.bin`
	- `wget https://www.espruino.com/binaries/espruino_2v03_esp8266/espruino_esp8266_user1.bin`
	- **Or, unzip from this repo and move the files to root:** `unzip espruino-2v03.zip && mv espruino-2v03/* . && rm -rf espruino-2v03 && rm -rf __MAC_OSX/`

5. Flash the firmware to the board.
	- Run `bash flash.sh`
	- This is the equivalent of the following:

	```
	esptool.py --baud 115200 --port /dev/tty.SLAB_USBtoUART write_flash -fs 4MB -ff 80m --flash_mode dio 0x0000 boot_v1.6.bin 0x1000 espruino_esp8266_user1.bin 0x3FC000 esp_init_data_default.bin 0x3FE000 blank.bin
	```
	
	- NOTE: If you are on a 512kb board your command will need to be different. Take a look [here](https://github.com/espruino/Espruino/blob/master/targets/esp8266/README_flash.txt).
	- I can't confirm this, but it will probably be something along these lines:

	```
	esptool.py --port /dev/tty.SLAB_USBtoUART --baud 115200 write_flash --flash_freq 40m --flash_mode dio --flash_size 4m 0x0000 boot_v1.6.bin 0x1000 espruino_esp8266_user1.bin 0x7C000 esp_init_data_default.bin 0x7E000 blank.bin
	```

6. You should see a confirmation that the board was successfully flashed. You're almost ready to open the board in the Espruino editor.
	- Before connecting your board to the editor, open up the Espruino Web IDE.
	- Go to `Settings > Communications` and set the `Baud Rate` to `115200`.
	- Connect your board to the IDE and you should be good to go. You can write code in the editor, flash it to the board, and interact with it as you would an Espruino board (with some caveats).
	- NOTE: If you go back to using a normal Espruino board you will need to return the `Baud Rate` to `9600`.


## Resources

[EspruinoESP8266](http://www.espruino.com/EspruinoESP8266)

[Espruino Binaries](http://www.espruino.com/Download)

[USB to UART Driver](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

[Flashing ESP8266 with Espruino](http://www.espruino.com/ESP8266_Flashing)

[Flashing with esptool.py](https://github.com/espruino/Espruino/blob/master/targets/esp8266/README_flash.txt)

[Video detailing the process](https://www.youtube.com/watch?v=j9xwgeE9u8E)

[Virtualenv/Virtualenv wrapper](https://docs.python-guide.org/dev/virtualenvs/#virtualenvwrapper)
