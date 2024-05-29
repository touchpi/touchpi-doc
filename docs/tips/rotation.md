# Offset, Rotation, Scaling

## Change rotation, stretch or reduce touchfield dimension

Get parameter for changing rotation, stretching or reducing touchfield dimension with this tool: 
[Editor for linux x11 xinput calibration](https://codepen.io/GottZ/full/pWpNgK). Some background information of this tool here:  
[github discussion](https://github.com/notro/fbtft/issues/445#issuecomment-334534400) 
and update your `/usr/share/X11/xorg.conf.d/40-libinput.conf` file.

Test with X window server in background
```
sudo -b /usr/lib/xorg/Xorg :0
```
Test with calling e.g. `DISPLAY=:0.0 xcalc`

if it does not fit, then kill X window server in background with `sudo kill <pid>`. 
You can get the pid with `ps -ef`.
Update your `/usr/share/X11/xorg.conf.d/40-libinput.conf` file.
And test again until it fits.

## Change x,y offset of the touchfield (calibrate)

Calibrate with xinput_calibrator

`xinput_calibrator -v --output-type xorg.conf.d`

copy output to `/usr/share/X11/xorg.conf.d/99-calibration.conf` file.
