# EFI for ASUS ROG STRIX B360

<!-- vim-markdown-toc GitLab -->

* [updates](#updates)
	* [Saturday March 16, 2019](#saturday-march-16-2019)
* [what doesn't work](#what-doesnt-work)
* [drivers64UEFI](#drivers64uefi)
	* [OsxAptioFix2Drv-free2000.efi](#osxaptiofix2drv-free2000efi)
* [kexts](#kexts)
	* [USBInjectAll](#usbinjectall)
	* [Various Lilu kexts](#various-lilu-kexts)
		* [AppleALC](#applealc)
		* [WhateverGreen](#whatevergreen)

<!-- vim-markdown-toc -->


## updates

### Saturday March 16, 2019

* This version now works with IGPU enabled and is much snappier than without.
* added bios folder with CMO settings as well as a text version

## what doesn't work

* onboard Wi-Fi
* USB 3.0

## drivers64UEFI

### OsxAptioFix2Drv-free2000.efi

The problem is that most X99 systems are allocating a lot of memory to PCIe
devices, and allocating the memory in many memory fragments rather than one
contiguous chunk.

The solution is to first free the first 512MB of fragmented memory which gives
ample room for the OS X kernel and kernel cache, then apply memory map fixes
which allow OS X to communicate with your installed hardware.

Download and place OsxAptioFix2Drv-free2000.efi in your /EFI/ClOVER/drivers64UEFI folder

Source: [https://nickwoodhams.com/x99-hackintosh-osxaptiofixdrv-allocaterelocblock-error-update/](https://nickwoodhams.com/x99-hackintosh-osxaptiofixdrv-allocaterelocblock-error-update/)

## kexts

### USBInjectAll

In 10.11+ Apple has changed significantly the way the USB drivers work. In the
absense of a port injector, the drivers use ACPI to obtain information about
which ports are active. Often, this information is wrong. Instead of correcting
the DSDT, a port injector can be used (just as Apple did for their own
computers). But in order to create such an injector, you must first determine
which ports are actually being used. And to do that you need to inject all
ports so you can test all ports on the computer to determine which ones
correspond to each available port address. You can't test a port that is
disabled...

That's where this kext comes in.

* [https://bitbucket.org/RehabMan/os-x-usb-inject-all](https://bitbucket.org/RehabMan/os-x-usb-inject-all)
* [https://github.com/RehabMan/OS-X-USB-Inject-All](https://github.com/RehabMan/OS-X-USB-Inject-All)



### Various Lilu kexts

An open source kernel extension bringing a platform for arbitrary kext,
library, and program patching throughout the system for macOS.

* [https://github.com/acidanthera/Lilu](https://github.com/acidanthera/Lilu)


#### AppleALC

An open source kernel extension enabling native macOS HD audio for not
officially supported codecs without any filesystem modifications

* [https://github.com/acidanthera/AppleALC](https://github.com/acidanthera/AppleALC)

#### WhateverGreen

Lilu plugin providing patches to select GPUs on macOS. Requires Lilu 1.2.5 or
newer.

* [https://github.com/acidanthera/WhateverGreen](https://github.com/acidanthera/WhateverGreen)
