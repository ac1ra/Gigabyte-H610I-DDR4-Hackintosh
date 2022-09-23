# GA-H610I-DDR4-Hackintosh
[GUIDE] Installing macOS Monterey (12.5.x) on Gigabyte H610I-DDR4 [OpenCore]

### Overview
[Thanks Fu-Yuxuan-hub for make EFI](https://github.com/Fu-Yuxuan-hub/General-EFI-for-H610-B660-Z690.git)

My computer Gigabyte H610I-DDR4 with MacOS 12.5.x. All devices work very well, without sleep-mode.

#### Performance
Pictures - Coming soon

#### Specs
- **CPU:** 12th Gen Intel(R) Core(TM) i3-12100F
- **RAM:** 2x32Gb DDR4 A-Data Premier [AD4U320032G22-SGN] 3200 Mhz
- **SSD:** 256Gb 2.5" Digma Run S9 DGSR2256GS93T, SATA III
- **GPU:** 8Gb Pulse AMD Radeon RX6600
- **Ports:** USB 2.0/USB 3.0/LAN/3'5 Jack

#### Don't work
- Sleep mode (Probable, I don't check)

#### BIOS settings

#####Disabled:
- Fast Boot
- VT-d (**enable if DisableMapper Quirks set True)** 
- CFG Lock
- Secure Boot
- Parallel Port
- Serial Port
- Resizable BAR Support

#####Enabled:
- VT-x
- UEFI startup mode
- Above 4G decoding
- Hyper-Threading
- Execute Disable Bit
- EHCI/XHCI Hand-off
- OS type: Windows 10 UEFI Mode
- PCI-e x16 switched to Gen3.0 (**If Videocard connect to PCI-e x16 Riser**)

#### Creating USB

**I recommend to create on the USB-flash with USB3.0, because the install will very long.** 

[**Read Dortania GUIDE:**](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#downloading-macos-modern-os)


#### Createinstallmedia method

This is the same mechanism you would use to create a USB installer for a real Mac Mojave.

It is a single line, executed in Terminal:

> sudo /Applications/Install\ macOS\ Monterey.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume

USB bootloader is ready.

#### Post Installation

After installation mount local EFI disk. Terminal:

> sudo dislutil list

> sudo diskutil mount disk0s1 (see diskutil list)

Copy EFI folder to EFI partition.

**OC - boot-args:**
> keepsyms=1 debug=0x100 agdpmod=pikera -wegnoigpu alcid=66

Reboot system. MacOS Monterey is ready.

#### Adding: Problem with hibernation ####

Everything required for CPU/IGPU power management is already installed with the steps above.
There is no longer any need to use the ssdtPRgen.sh script.

Be aware that hibernation (suspend to disk or S4 sleep) is not well supported on hackintosh.

You should disable it:
Code:
> sudo pmset -a hibernatemode 0
 
> sudo rm /var/vm/sleepimage

> sudo mkdir /var/vm/sleepimage

Always check your hibernatemode after updates and disable it. System updates tend to re-enable it, although the trick above (making sleepimage a directory) tends to help.

**Enjoy it!**