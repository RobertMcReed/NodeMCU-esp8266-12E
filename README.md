# Setting up NodeMCU ESP8266-12E

1. Download [USB to UART Bridge VCP Driver](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers) and install the driver.
	- [Direct download for MAC](https://www.silabs.com/documents/public/software/Mac_OSX_VCP_Driver.zip)
	- `wget https://www.silabs.com/documents/public/software/Mac_OSX_VCP_Driver.zip`
	- **Or use the included file.** 

		```
		unzip Mac_OSX_VCP_Driver.zip && open Mac_OSX_VCP_Driver/SiLabsUSBDriverDisk.dmg
		```
	
2. Plug in your board and verify it's COM Address.
	- `sudo ls /dev/tty.*`
	- You may need to enter your admin password
	- You should see `/dev/tty.SLAB_USBtoUART` listed. If not, verify the driver was installed correctly. You may need to grant privileges to it in security settings.

3. Download the Python tools for flashing the firmware to the board.
	- Create a virtualenv to stay clean: `mkvirtualenv esp8266`
	- Download esptool and pyserial: `pip install esptool pyserial`
	- **Alternatively, using this repo:** `pip install -r requirements.txt`
	- **If you encounter problems, try with python 2.7**

4. Erase the flash memory on the board.
		```
		esptool.py --port /dev/tty.SLAB_USBtoUART --baud 115200 erase_flash
		```

5. Continue to either the [arduino README](arduino/README.md) or [espruino README](espruino/README.md) to flash your board with the appropriate firmware.


## Resources

[USB to UART Driver](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

[Virtualenv/Virtualenv wrapper](https://docs.python-guide.org/dev/virtualenvs/#virtualenvwrapper)

[Amazon ESP8266](https://www.amazon.com/gp/product/B01IK9GEQG/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)

[ESP8266 Guide](https://tttapa.github.io/ESP8266/Chap01%20-%20ESP8266.html)
