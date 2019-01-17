# KaRadio32 on ODROID-GO

odroid.csv and builds/odroid.bin could be using for to install [KaRadio32](https://github.com/karawin/Ka-Radio32) on [ODROID-GO](https://www.hardkernel.com/shop/odroid-go/) device.

---------------
Key map
---------------
In odroid.csv is defined following configuration:

Key label    | Mapping
-------------|----------------------------------------------------------------------------------
"Menu"       | P_BTN0_A short click: start/stop, long click: toggle, double click: display info;
"Volume"     | P_BTN1_A short click: start/stop, long click: toggle, double click: display info;
"Select"     | P_BTN1_C previous station (or volume up when "Menu" or "Volume" is toggled);
"Start"      | P_BTN1_B next station (or volume down when "Menu" or "Volume" is toggled);
"A"          | P_BTN0_C volume down (or previous station when "Menu" or "Volume" is toggled);
"B"          | P_BTN0_B volume up (or next station when "Menu" or "Volume" is toggled);

Remark: on my device "Volume" does not working.

----------------
Flashing
----------------
For install KaRadio32 on your ODROID-GO do following steps:
1. Install "ESP32 download tool" (you can take it here <http://espressif.com/en/support/download/other-tools>);
2. You might need to install the [USB-UART CP2104 VCP driver for Windows](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers) when the ODROID turns on.
3. Download binaries from <https://github.com/karawin/Ka-Radio32/tree/master/binaries>;
4. Download odroid.bin from <https://github.com/karawin/Ka-Radio32/tree/master/boards/build>;
5. Download factory firmware from <https://github.com/OtherCrashOverride/odroid-go-firmware/releases> (for if you want [return device to factory state](https://wiki.odroid.com/odroid_go/firmware_update));
6. Turn on your ODROID-GO, plug it in your PC, start ESP download tool.
7. Flash binaries to your device as described [here](https://wiki.odroid.com/odroid_go/firmware_update), but use following files and adresses:

File                           | Adress
-------------------------------|---------
KaRadio32.bin                  | 0x10000
KaRadio32v1.6r3.bin (or newer) | 0x1d0000
partitions.bin                 | 0x8000
bootloader.bin                 | 0x1000
odroid.bin                     | 0x3a2000

![Screenshoot of download tool](https://github.com/pepelnyy/KaRadio32-on-ODROID-GO/raw/master/Images/Screenshot%20of%20ESP32%20DOWNLOAD%20TOOL.png)

----------------
On first start after flashing
----------------

- Connect your device to your PC and establish serial connection (use [Termite](https://www.compuphase.com/software_termite.htm), for example)
- If the acces point of your router is not known, the webradio inits itself as an AP. Connect the wifi of your computer to the ssid "WifiKaRadio"  
- Browse to 192.168.4.1 to display the page, got to "setting" "Wifi" and configure your ssid ap, the password if any, the wanted IP or use dhcp if you know how to retrieve the dhcp given ip (terminal or scan of the network).
- In the gateway field, enter the ip address of your router.
- Validate. The equipment restart to the new configuration.
- Put following commands in serial terminal
- The device's screen have to show something
- If nothing happens try telnet
- Connect your wifi to your AP
- You can find IP adress of your device in serial output
- Connect to your device by telnet using this IP and port 23 (use [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), for example).
- Put following commands in console

```
sys.lcd("194")
sys.rotat("1")
sys.tzo("x") where x is your time offset
sys.ledgpio("2")
sys.lcdout("x")	: Timer in seconds to switch off the lcd. 0= no timer
```

- Run browser and browse to the ip given in configuration.
- Choose "DAC" on "Settings" page and validate changes.
![Screenshot of "Settings"](https://github.com/pepelnyy/KaRadio32-on-ODROID-GO/raw/master/Images/WebPage.png)
- Congratulation, you can edit your own station list. Dont forget to save your stations list in case of problem or for new equipments.
- if the AP is already known by the esp32, the default ip is given by dhcp.
- a sample of stations list is on http://karadio.karawin.fr/WebStations.txt . Can be uploaded via the web page.

## ENJOY!

