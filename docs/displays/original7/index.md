# Original Raspberry 7 inch Touch Display 

Set up an original Raspberry 7 inch touch display mounted on a Raspberry 4B for touchpi.<br> 
Tested with Raspberry Pi OS Bookworm Lite.<br>
<ins>We accept no liability for any problems that may arise when following this procedure.</ins>

![touchpi @ original 7 inch display with Raspi 4B](../../img/RPi4_original7_1.jpg)

/// note
There is now driver installation necessary. Everything works out of the box.<br>
Because of the used hardware case, it was necessary to rotate the display 180 degrees.
///

## Install Image
It is a good idea to save some system files after installation and first boot of the Raspberry Pi OS Bookworm Lite image. 
Image installation is described here: [Installation](../../index.md#install).

/// details | Origin /boot/cmdline.txt 
```
--8<-- "./docs/displays/original7/cmdline.txt"
```
///

/// details | Origin /boot/config.txt 
``` linenums="1"
--8<-- "./docs/displays/original7/config.txt"
```
///

``` title="Update OS with"
sudo apt update && sudo apt upgrade --yes
sudo apt install --yes --no-install-recommends git xorg x11-apps xinput-calibrator
```

Changes in /boot/cmdline.txt with
```
sudo nano /boot/cmdline.txt
```
add ` video=DSI-1:800x480@60,rotate=0` to the end of the line.
This change is not needed, but makes your cmdline.txt more readable. 
Especially when you want to rotate your display.  

/// details | Changed /boot/cmdline.txt 
```
--8<-- "./docs/displays/original7/cmdline.changed.txt"
```
///

Reboot 
```
sudo reboot
```
Run X window server in background
```
sudo -b /usr/lib/xorg/Xorg :0
```
test with calling e.g. `DISPLAY=:0.0 xcalc`

## Rotation (screen and touch)
You can rotate the touch display with changes in the `boot/cmdline.txt` and `/usr/share/X11/xorg.conf.d/40-libinput.conf` file.
Edit with `sudo nano`.

| /boot/cmdline.txt                                                              | /usr/share/X11/xorg.conf.d/40-libinput.conf                                                          |
|--------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| ` video=DSI-1:800x480@60,rotate=0`<br>(power connector down)                   | `Option "TransformationMatrix" "1 0 0 0 1 0 0 0 1"`<br>Option is optional. Not needed in the file. |
| ` video=DSI-1:800x480@60,rotate=90`<br>(power connector left)                  | Use TransformationMatrix 90 -><br>`Option "TransformationMatrix" "0 1 0 -1 0 1 0 0 1"`                  |                               
| ` video=DSI-1:800x480@60,rotate=180`<br>(power connector up, preferred layout) | Use TransformationMatrix 180 -><br>`Option "TransformationMatrix" "-1 0 1 0 -1 1 0 0 1"`                |
| ` video=DSI-1:800x480@60,rotate=270`<br>(power connector right)                | Use TransformationMatrix 270 -><br>`Option "TransformationMatrix" "0 -1 1 1 0 0 0 0 1"`                 |

/// details | Origin /usr/share/X11/xorg.conf.d/40-libinput.conf
``` linenums="1"
--8<-- "./docs/displays/original7/40-libinput.conf"
```
///

/// details | Changed /usr/share/X11/xorg.conf.d/40-libinput.conf 
``` linenums="1"  hl_lines="43"
--8<-- "./docs/displays/original7/40-libinput.changed.conf"
```
///


Read more about offsets, scaling and rotation [here](../../tips/rotation.md).