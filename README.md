# Wine
Wine (originally an acronym for "Wine Is Not an Emulator") is a compatibility layer capable of running Windows applications on several POSIX-compliant operating systems, such as Linux, Mac OSX, & BSD. Instead of simulating internal Windows logic like a virtual machine or emulator, Wine translates Windows API calls into POSIX calls on-the-fly, eliminating the performance and memory penalties of other methods and allowing you to cleanly integrate Windows applications into your desktop.
 
For more information, please visit: http://www.winehq.org.
 
 
## About
I made the binary package (*.deb) for personal use only. Because the wine package in Debian Stable (Wheezy) official repository still has 1.4.1 version. But the wine stable package now has 1.6.2 version.
 
The binary package was compiled using Linux Debian 7 64-bit with debootsrap and schroot methods. It runs smoothly on my computer (Debian 7 64-bit) and notebook (Debian 7 32-bit).
 
Many users prefer to use 32-bit wine package in their 64-bit Debian, because the compatibility with some wine's programs (example: Microsoft Office).
 
 
## Installation
Use these commands as *root user*.
 
* Install wine.
  ```
  dpkg -i wine_1.6.2-1_i386.deb
  ```
  
* Install some dependencies.
  ```
  apt-get install lib32ncurses5 libgstreamer-plugins-base0.10-0:i386 winbind
  ```
  

## Wine Mono and Wine Gecko
As a *normal user*, make sure there's *wine* directory inside the *.cache* directory.
Then copy these .msi files (*wine-mono-0.0.8.msi* and *gecko-2.21-x86.msi*) into the directory:
```
~/.cache/wine/
```
This step is an **alternative**, usually wine will automatically download these files for you.
  
  
## Tricks for Linux Debian 64-bit
Use these commands as *root user*.
 
* **Missing some 32-bit libraries?** Enable *multiarch* and install additional 32-bit libraries.
  ```
  dpkg --add-architecture i386 && apt-get update && apt-get install ia32-libs
  ```
  
* Fix *gnome-keyring* for wine 32-bit at Linux Debian 64-bit.
  * Download *gnome-keyring* package for 32-bit architecture.
    ```
    apt-get download gnome-keyring:i386
    dpkg -x gnome-keyring_*.deb gnome-keyring
    cp -r gnome-keyring/usr/lib/i386-linux-gnu/pkcs11 /usr/lib/i386-linux-gnu/
    ```
 
  * Check the DE (Desktop Environment) that you use in file: 

    */etc/xdg/autostart/gnome-keyring-pkcs11.desktop*
 
    Search for line:
    ```
    OnlyShowIn=
    ```
    For example, I'm using MATE, so I add/modify that line: 
    ```
    OnlyShowIn=MATE;
    ```
  

## Create 32-bit Wine Prefix
Use these commands as *normal user*.
  
1.  For example, *~/.wine-programs* is your directory location for program installation.
     Use this command to make the directory:
     ```
     env WINEARCH=win32 WINEPREFIX=~/.wine-programs winecfg
     ```

2.  */location/to/setup.exe* is the setup file location. Then install the program with this command:
     ```
     env WINEARCH=win32 WINEPREFIX=~/.wine-programs wine /location/to/setup.exe
     ```
