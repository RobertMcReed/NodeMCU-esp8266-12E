# Arduino on NodeMCU ESP8266-12E

1. Follow the setup procedure from the [main readme](../README.md).

2. Download the latest `dev` firmware from [github](https://github.com/nodemcu/nodemcu-firmware/releases?after=1.5.4.1-master_20161201):
	- `wget https://github.com/nodemcu/nodemcu-firmware/releases/download/0.9.6-dev_20150704/nodemcu_float_0.9.6-dev_20150704.bin`
	- **Or, use the file from this repo** 

3. Flash the firmware to the board.
		```
		esptool.py --baud 115200 --port /dev/tty.SLAB_USBtoUART write_flash -fs 4MB -ff 80m --flash_mode dio 0x00000 nodemcu_float_0.9.6-dev_20150704.bin
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
	
4. Download the [Arduino editor](https://www.arduino.cc/en/Main/Software).
5. Set up the editor for the NodeMCU:
   1. `Arduino > Preferences > Additional Boards Manager URLs:`

	 		- Paste `http://arduino.esp8266.com/stable/package_esp8266com_index.json`
   2. `Tools > Boards > Boards Manager`
	 
	 		- Search for `esp8266` and click `esp8266 by ESP8266 Community`
	 		- Click `Install`
   3. Select and setup the board.
	
			- `Tools > Board > NodeMCU 1.0 (ESP - 12E Module)`
			- `Tools > Upload Speed > 921600`
			- `Tools > CPU Frequency > 80 MHz`
			- `Tools > Flash Size > 4M (3M SPIFFS)`
			- `Tools > Port > /dev/cu.SLAB_USBtoUART`
   4. Write your code, then upload it to the board!



## Resources

[Servo Instructable](https://www.instructables.com/id/Interfacing-Servo-Motor-With-NodeMCU/)

[NodeMCU Binaries](https://github.com/nodemcu/nodemcu-firmware/releases/)

[Video detailing the process](https://www.youtube.com/watch?v=MHrm7axsImI)
