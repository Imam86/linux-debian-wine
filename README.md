# Wine
# =====
Wine (originally an acronym for "Wine Is Not an Emulator") is a compatibility layer capable of running Windows applications on several POSIX-compliant operating systems, such as Linux, Mac OSX, & BSD. Instead of simulating internal Windows logic like a virtual machine or emulator, Wine translates Windows API calls into POSIX calls on-the-fly, eliminating the performance and memory penalties of other methods and allowing you to cleanly integrate Windows applications into your desktop.

For more information, please visit: http://www.winehq.org.

This binary package (*.deb) was compiled using Debian 7 64-bit with debootsrap and schroot methods. 

### Installation
### =======
Install as *root user* with this command:
```
dpkg -i wine_1.6.2-1_i386.deb
```

### Tricks for Linux Debian 64-bit
### ==================
Use these command as *root user*.

* Enable *multiarch*.
```
dpkg --add-architecture i386 && apt-get update
```

* Install additional packages.
```
apt-get install ia32-libs lib32ncurses5 libgstreamer-plugins-base0.10-0:i386
```

* Fix for *gnome-keyring* wine 32-bit at Linux Debian 64-bit.
  * Download gnome-keyring packages for 32-bit architecture
```
apt-get download gnome-keyring:i386
dpkg -x gnome-keyring_*.deb gnome-keyring
cp -r gnome-keyring/usr/lib/i386-linux-gnu/pkcs11/ /usr/lib/i386-linux-gnu/
```

  * Check the DE (Desktop Environment) that you use in file: */etc/xdg/autostart/gnome-keyring-pkcs11.desktop*
Search for line:
```
OnlyShowIn=
```
For example, I'm using MATE, so I add/modify that line: 
```
OnlyShowIn=MATE;
```
