##Rotating the screen
edit _/boot/config.txt_:
````
sudo nano /boot/config.txt
````
Add the following line:
````
display_rotate=1
````

##Autohiding the Mouse Cursor
Install _unclutter_: 
````
sudo apt-get install unclutter
````
__version 1 only__
##Disabling the screensaver

edit _/etc/xdg/lxsession/LXDE-pi/autostart_:
````
sudo nano /etc/xdg/lxsession/LXDE-pi/autostart
````
Add the following lines:
````
@xset s noblank
@xset s off
@xset -dpms
````

Edit _/etc/lightdm/lightdm.conf_:
````
sudo nano /etc/lightdm/lightdm.conf
````
Add the following line below [SeatDefaults]
````
xserver-command=X -s 0 -dpms
````

## Disable WiFi Power Save

Edit _/etc/modprobe.d/8192cu.conf_
```shell
sudo nano /etc/modprobe.d/8192cu.conf
```

Add the following lines
```shell
# Disable power saving
options 8192cu rtw_power_mgnt=0 rtw_enusbss=1 rtw_ips_mode=1
```

**For Raspberry Pi 3**  
Edit _/etc/network/interfaces_
```shell
sudo nano /etc/network/interfaces
```

Add the following line under the _wlan0_ section
```shell
wireless-power off
```

Reboot your PI
```shell
sudo reboot
```

## Enable file sharing with OS X

Install _Netatalk_:
````
sudo apt-get install netatalk
````

## Enable VNC

Install _x11vnc_:
````
sudo apt-get install x11vnc
````

Set VNC password:
````
x11vnc -storepasswd
````

Create an auto-start file:
````
cd ~/.config
mkdir autostart
cd autostart
nano x11vnc.desktop
````

Add the following lines:
````
[Desktop Entry]
Encoding=UTF-8
Type=Application
Name=X11VNC
Comment=
Exec=x11vnc -forever -usepw -display :0 -ultrafilexfer
StartupNotify=false
Terminal=false
Hidden=false
````
