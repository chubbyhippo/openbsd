# openbsd
## doas
usermod -G wheel mynewuser

### /etc/doas.conf
permit nopass :wheel  
permit nopass mynewuser

## apmd
rcctl enable apmd  
rcctl set apmd flags -A -z 10  
rcctl start apmd  

## external display
xrandr -q  
xrandr --output LVDS-1 --off  
xrandr --output LVDS-1 --auto  
xrandr --output HDMI-2 --auto --right-of eDP-1  
xrandr --output HDMI-1 --auto --rotate left --right-of HDMI-2 
 
## keyboard layouts
setxkbmap -layout us,th  
setxkbmap -option 'grp:caps_toggle'

## turn off bell sound
xset b off

## fontunsupported_browser
xset fp default  
for font in /usr/local/share/fonts/* ; do  
&nbsp;&nbsp;&nbsp;&nbsp;xset fp+ $font  
done  
xset fp rehash  

## lock screen
xidle -delay 5 -sw -program "/usr/X11R6/bin/xlock" -timeout 300  

## connect wifi
ifconfig iwn0 up  
ifconfig iwn0 nwid ID wpakey KEY  
dhclient iwn0  

## find disks/usb devs
sysctl hw.diskcount  
sysctl hw.disknames
disklabel sd1  

## fix tearing intel
### /etc/X11/xorg.conf.d/intel.conf
Section "Device"  
&nbsp;&nbsp;Identifier "drm"  
&nbsp;&nbsp;Driver "intel"  
&nbsp;&nbsp;Option "TearFree" "true"  
EndSection  

## $HOME/.xsession
setxkbmap -layout us,th  
setxkbmap -option 'grp:caps_toggle'  
xset b off  
xset fp default  
for font in /usr/local/share/fonts/* ; do  
&nbsp;&nbsp;&nbsp;&nbsp;xset fp+ $font  
done  
xset fp rehash  
xsetroot -solid black &  
xterm -bg black -fg white +sb &  
xidle -delay 5 -sw -program "/usr/X11R6/bin/xlock" -timeout 300 &  
cwm

## $HOME/.cwmrc
command term "xterm -bg black -fg white +sb"  
command firefox /usr/local/bin/firefox  
command chrome /usr/local/bin/chrome  

bind-key 4-h window-snap-left  
bind-key 4-j window-snap-down  
bind-key 4-k window-snap-up  
bind-key 4-l window-snap-right  
