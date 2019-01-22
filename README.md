# Ka-Radio32 on ODROID-GO

odroid.csv and builds/odroid.bin could be using for to install [Ka-Radio32](https://github.com/karawin/Ka-Radio32) by [**KaraWin**](https://github.com/karawin) on [ODROID-GO](https://www.hardkernel.com/shop/odroid-go/) device.

### Remarks
1. On this stage it is necessary to reflash whole device to switch from default firmware to KaRadio32 and back.
2. The sound quality on built-in speaker is not very good. I strongly recommend to use some external DAC. I will tell about it [below](https://github.com/pepelnyy/KaRadio32-on-ODROID-GO/blob/master/README.md#using-of-external-dac).

## Key map

In odroid.csv is defined following configuration:

Key label    | Mapping
-------------|----------------------------------------------------------------------------------
"Menu"       | P_BTN0_A short click: start/stop, long click: toggle, double click: display info;
"Volume"     | P_BTN1_A short click: start/stop, long click: toggle, double click: display info;
"Select"     | P_BTN1_C previous station (or volume up when "Menu" or "Volume" is toggled);
"Start"      | P_BTN1_B next station (or volume down when "Menu" or "Volume" is toggled);
"A"          | P_BTN0_C volume down (or previous station when "Menu" or "Volume" is toggled);
"B"          | P_BTN0_B volume up (or next station when "Menu" or "Volume" is toggled);
"Up" and "Down" | P_JOY_0 controls volume up and down;
"Left" and "Right" | P_JOY_1 switch previous or next station.

Remark: on my device button "Volume" does not working.

## Flashing

For install KaRadio32 on your ODROID-GO do following steps:
1. Install "ESP32 download tool" (you can take it here <http://espressif.com/en/support/download/other-tools>);
2. You might need to install the [USB-UART CP2104 VCP driver for Windows](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers) when the ODROID turns on.
3. Download binaries from <https://github.com/karawin/Ka-Radio32/tree/master/binaries>;
4. Download odroid-go.bin from <https://github.com/karawin/Ka-Radio32/tree/master/boards/build>;
5. Download factory firmware from <https://github.com/OtherCrashOverride/odroid-go-firmware/releases> (for if you want [return device to factory state](https://wiki.odroid.com/odroid_go/firmware_update));
6. Turn on your ODROID-GO, plug it in your PC, start ESP download tool.
7. Flash binaries to your device as described [here](https://wiki.odroid.com/odroid_go/firmware_update), but use following files and adresses:

File                           | Adress
-------------------------------|---------
KaRadio32.bin                  | 0x10000
KaRadio32v1.6r4.bin (or newer) | 0x1d0000
partitions.bin                 | 0x8000
bootloader.bin                 | 0x1000
odroid-go.bin                  | 0x3a2000

![Screenshoot of download tool](https://github.com/pepelnyy/KaRadio32-on-ODROID-GO/raw/master/Images/Screenshot%20of%20ESP32%20DOWNLOAD%20TOOL.png)

## On first start after flashing

- If the acces point of your router is not known, the webradio inits itself as an AP. Connect the wifi of your computer to the ssid "WifiKaRadio"  
- Browse to 192.168.4.1 to display the page, got to "setting" "Wifi" and configure your ssid ap, the password if any, the wanted IP or use dhcp if you know how to retrieve the dhcp given ip (terminal or scan of the network).
- In the gateway field, enter the ip address of your router.
- Validate. The equipment restart to the new configuration.
- Connect your wifi to your AP
- if the AP is already known by the esp32, the default ip is given by dhcp.
- You can find IP adress of your device on screen
- Run browser and browse to the ip given in configuration.
- Choose "DAC" on "Settings" page and validate changes. Your device will restart.
![Screenshot of "Settings"](https://github.com/pepelnyy/KaRadio32-on-ODROID-GO/raw/master/Images/WebPage.png)
- Refresh page. On "Settings" page you can ajust your Time Zone Offset (don't forget push "Validate").
- Congratulation, you can edit your own station list. Dont forget to save your stations list in case of problem or for new equipments.
- a sample of stations list is on http://karadio.karawin.fr/WebStations.txt . Can be uploaded via the web page.
- If you want to change time before screen will turn off when device is inactive
- Connect to your device by telnet using this IP and port 23 (use [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), for example).
- Put following command in console

```
sys.lcdout("x")	: Timer in seconds to switch off the lcd. 0= no timer
```

## Using of external DAC

For improvement the sound you can use the [external I2S DAC](https://forum.odroid.com/viewtopic.php?f=158&t=31853#p231211)
To activate it you will need to edit the [odroid.csv](https://github.com/karawin/Ka-Radio32/tree/master/boards) according your wiring and compile and flash new odroid.bin to your device. You can learn how to do it [here](https://github.com/karawin/Ka-Radio32/blob/master/HardwareConfig.md#hardware-configuration-partition).

[_Back_](https://github.com/pepelnyy/KaRadio32-on-ODROID-GO/blob/master/README.md#remarks)

## ENJOY!

https://youtu.be/uuBrMle3xsQ
