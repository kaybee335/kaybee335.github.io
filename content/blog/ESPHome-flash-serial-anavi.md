Title: Summary for flashing Anavi ESPs with µART
Date: 2022-03-31
Category: blog
Tags: reference, quick_ref, ESPHome, Basic
Slug: ESPHome-anavi-serial-flash
Author: kaybee335
Summary: Quick reference for initial serial flash of Anavi ESP devices.  Uses µART as USB-Serial UART.

# Steps:
- Prepare initial ESPHome YAML configuration file using the ESPHome Wizard for `ESP8266` and `esp12e` as the platform and board. Compile (don't Run) the YAML file.
```
> esphome wizard your-project-name.yaml
   ... wizard configuration dialog
   ...
> esphome compile your-project-name.yaml
```
- Connect μArt to (powered off) Anavi board using flying leads, **RX-TX crossover**, 3.3VDC, GND. Connect computer USB to μArt microUSB.
- Run the YAML. This should compile/link cleanly and initiate the upload. Select the serial port for the μArt when prompted and hit enter.  The upload shoud start after some initial negotiation with the board bootloader. **Keep** holding the microswitch down until flashing is complete. The board will reset but will not reboot. When the board has reset release the Reset microswitch.
- Cycle power on the Anavi board with the μArt still connected and the `esphome` program still running.  You should see log output as the board reboots and initialises various ESPHome components. Verify successful WiFi connection n the log.
- Power down the Anavi board. Unplug μArt from computer USB. Apply power to the Anavi board.
- `esphome run` the YAML file again. The μArt serial port will not be detected by ESPHome and will usually proceed directly to OTA uploading depending on your COM port configuration, otherwise you can select OTA.
```
> esphome run your-project-name.yaml
```

- Once flashing is complete, the board will reset and reboot properly.The console should shortly start showing logging information over the WiFi connection to the board.

# µART Connection

**Pin mapping:**


| μArt lead | Anavi Pin Header
| :-------- | :---------------
| VIN       | 3.3V
| GND       | GND
| TXD >>    | RX
| << RXD    | TX


**Header board Location:**

![Anavi ESP connection](../images/muart_header_connect.png "Anavi ESP connection")

