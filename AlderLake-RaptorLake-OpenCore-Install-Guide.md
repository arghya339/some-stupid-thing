

# OpenCore Alder Lake (12th-Gen Intel) / Raptor Lake (13/14th-Gen Intel)  Hackintosh Guidance

## 🪧Install macOS on 12th/13th/14th Gen Intel CPUs using OpenCore from Windows

## [📝Terminology](https://dortania.github.io/OpenCore-Install-Guide/terminology.html)

<details><summary>

## 🖥️Actual Hardware used
</summary>

### Motherboards

Mostly Z690/Z790 and B660M/B760, also a few Hackintosh seen yet with H610/H710 and H670/H760. Gigabyte and Asus and MSI and ASRock have been used in the great majority of observed systems. macOS on Alder Lake or Raptor Lake laptops is not possible, due to the unsupported iGPU.

- Gigabyte B660M DS3H AX DDR4 (rev 0/1/2)

### CPUs actually used

All currently available Alder Lake /  Raptor Lake Core-ix-12/13/14xxx CPUs should work. 

- Intel Core i3-12100F

### GPUs actually used

In the context of Alder Lake, I have seen primarily recommended: AMD RX 400 series, RX 500 series, RX 5000 series, RX 6800, RX 6800 XT, RX 6900 XT. AMD RX 6600 and 6600 XT are only supported in Monterey 12.1 and newer. (But RX 7900 XT is currently not supported at all.)

- Sapphire Pulse Radeon RX 550 4GB GDDR5 (Lexa)

### SSDs actually used

Some Samsung NVMe drives may still have problems: SSD boot time tests · dortania. 

- WD Blue SN570 NVMe 500 GB

### Wifi Cards actually used

The recommendations: Intel AX101 M.2 WiFi 6E; Intel AX200 M.2 WiFi 6E; Intel AX201 M.2 WiFi 6E; Intel AX210 M.2 WiFi 6E, Intel AX411 M.2 WiFi 6E, Intel BE200 M.2 WiFi 7.

- Intel AX211 M.2 WiFi 6E 

### Wired Networking Controller

- Realtek RTL8125 2.5GBit Ethernet

This Controller is commonly used in many mid-range motherboards

### Onboard Audio Codec

- Realtek ALC897

This audio chip is commonly used in many mid-range motherboards

### OS used

- Sonoma 14

</details>

<details><summary>

## 🚫Things that don't work
</summary>

- [Sidecar](https://support.apple.com/en-in/102597) requires either an iGPU or an Apple T2 chip for HEVC encoding/decoding so it does not work on this system (iGPU UHD 770 is not supported by macOS). Alternatives to Sidecar: [Luna Display](https://apps.apple.com/us/app/luna-display/id1250259715) and [Duet Display](https://apps.apple.com/us/app/duet-display/id935754064).
- macOS treats all cores the same and does not schedule tasks optimally between P-cores and E-cores.
- Airdrop requires an Broadcom chip, so it does not work on this system (Intel Wireless ie. Intel AX211 is not supported for Airdrop by macOS). Alternatives to Airdrop: [LocalSend - App Store](https://apps.apple.com/us/app/localsend/id1661733229)|[LocalSend - PlayStore](https://play.google.com/store/apps/details?id=org.localsend.localsend_app)|LocalSend ~ `winget install LocalSend.LocalSend`|[LocalSend - FlatHub](https://flathub.org/apps/org.localsend.localsend_app).
- Location service on Apple Maps & to use GPS location on [QGIS](https://qgis.org/download/)  used [GPSD](https://formulae.brew.sh/formula/gpsd#default)

</details>

<details><summary>
    
## [🔍Finding Hardware](https://dortania.github.io/OpenCore-Install-Guide/find-hardware.html#finding-hardware-using-windows)
</summary>

[OpCore-Simplify](https://github.com/lzhoang2801/OpCore-Simplify): Export hardware report (Compatibility Checker script)

### [Finding CPU Model using Device Manager.png](https://dortania.github.io/OpenCore-Install-Guide/assets/img/cpu-model-devicemanager.e6eedd26.png)

### [Finding GPU Model using Device Manager.png](https://dortania.github.io/OpenCore-Install-Guide/assets/img/GPU-model-devicemanager.677068d3.png)

### [Finding Chipset Model using Device Manager.png](https://dortania.github.io/OpenCore-Install-Guide/assets/img/chipset-model-devicemanager.57f025ae.png)

### [Finding Audio Codec using Device Manager.png](https://dortania.github.io/OpenCore-Install-Guide/assets/img/audio-controller-aida64.png.bf36cd98.png)

### [Finding Network Controller models using Device Manager.png](https://dortania.github.io/OpenCore-Install-Guide/assets/img/nic-model-devicemanager.9bc7b615.png)

### [Finding Wireless Network Controller models using Device Manager.png](https://community.intel.com/t5/Wireless/Intel-R-Wi-Fi-6E-AX211-160MHz-Netwtw12-Network-adapter-can-t/m-p/1529172?lightbox-message-images-1529172=46300i03FF2F5A58CD3DF9)

### [Finding Drive Model using Device Manager.png](https://dortania.github.io/OpenCore-Install-Guide/assets/img/disk-model-devicemanager.41243ee5.png)
</details>

<details><summary>

## 💿Creating the USB 
</summary>

### [Making the installer in Windows](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/windows-install.html#downloading-macos)

While you don't need a fresh install of macOS to use OpenCore, some users prefer having a fresh slate with their boot manager upgrades.

To start you'll need the following:

- min 4GB USB Stick
- require [Python 3 installed](https://www.microsoft.com/store/productId/9PNRBTZXMB4Z)
- [macrecovery.py](https://github.com/acidanthera/OpenCorePkg/releases)

#### [Downloading macOS.gif](https://dortania.github.io/OpenCore-Install-Guide/assets/img/open-cmd-current-folder.906148d4.gif)

To grab legacy installers is super easy, first grab a copy of [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg/releases) and head to `/Utilities/macrecovery/`. Next, click next to the current folder path and type cmd to open a Command Prompt in the current directory:

Now run one of the following depending on what version of macOS you want(Note these scripts rely on [Python 3](https://www.microsoft.com/store/productId/9PNRBTZXMB4Z) support, please install if you haven't already):

##### [Monterey (12)](https://apps.apple.com/us/app/macos-monterey/id1576738294) | Discontinued for security updates (Apple ending official support after November 2024)
```py
python macrecovery.py -b Mac-FFE5EF870D7BA81A -m 00000000000000000 download
```
##### [Ventura (13)](https://apps.apple.com/us/app/macos-ventura/id1638787999) | Discontinued for security updates (Apple ending official support after November 2025)
```py
python macrecovery.py -b Mac-4B682C642B45593E -m 00000000000000000 download
```
##### [Sonoma (14)](https://apps.apple.com/us/app/macos-sonoma/id6450717509) | Recommended
```py
python macrecovery.py -b Mac-226CB3C6A851A671 -m 00000000000000000 download
````
##### [Sequoia (15)](https://apps.apple.com/us/app/macos-sequoia/id6596773750) | Stable
```py
python macrecovery.py -b Mac-937A206F2EE63C01 -m 00000000000000000 download
```
##### [Tahoe (26)](https://www.apple.com/in/os/macos/) | Latest
```py

```

- macOS 12 and above note: As recent macOS versions introduce changes to the USB stack, it is highly advisable that you map your USB ports (with `USBToolBox`) before installing macOS.

  > [!CAUTION]
  > With macOS 11.3 and newer, [`XhciPortLimit` is broken resulting in boot loops](https://github.com/dortania/bugtracker/issues/162).
    - If you've already [mapped your USB ports](https://dortania.github.io/OpenCore-Post-Install/usb/) and disabled `XhciPortLimit`, you can boot macOS 11.3+ without issues.
This will take some time, however once you're finished you should get either [`BaseSystem`](https://dortania.github.io/OpenCore-Install-Guide/assets/img/basesystem-example.93778929.png) or [`RecoveryImage`](https://dortania.github.io/OpenCore-Install-Guide/assets/img/macrecovery-after.4c24ba88.jpg) files:


> Now with our installer downloaded, we'll next want to format our USB Drive.

#### [Rufus method.png](https://dortania.github.io/OpenCore-Install-Guide/assets/img/format-usb-rufus.43feba9e.png)

1. Download & Open [Rufus](https://github.com/pbatard/rufus/releases)
2. Select USB Stick
3. Set the BOOT selection as `Non bootable`
4. Set Partition scheme as `GPT`
5. Volume label as `USB DRIVE`
6. Set File System as Large `FAT32`
7. Click `Start`
8. Delete all file autorun in USB Drive partition

<details><summary>

#### Format our USB Drive using Windows built-in tool
</summary>
    
#### Disk Management method

> [!TIP]
> possible to format a `USB Drive` as `FAT32` using Windows built-in `Disk Management`, it won't work if the drive is larger than 32GB. If your `USB Drive` is larger than 32GB Windows `Disk Management` won't allow you to format it as `FAT32` directly. You'll need to use other methods like: [Rufus](https://github.com/pbatard/rufus/releases) or `DiskPart`.

- Right click the Windows `Start` Button on your task bar and select `Disk Management`.
> If you have multiple `partitions` on the `USB Drive`, right click each partition and click `Delete Volume` for your `USB Drive` (This will remove data, make sure you have backups and only remove `partitions` from your `USB Drive`)
- You should see all of your `partitions` and `disks`. On the bottom half, you'll see your devices. Find your `USB Drive`.
- You'll want to `format` the `USB Drive` to have a `File system` : `FAT32` partition & `Volume label`: `USB Drive`.

#### DiskPart method

> This is a more advanced method but allows you to format larger than 32GB drives as FAT32.

- Open Command Prompt as administrator:
  - Press the `Windows` key.
  - Type `cmd` in the search bar.
  - Right-click on `Command Prompt` and select `Run as administrator`.
- Start DiskPart:
  - In the `Command Prompt` window, type `diskpart` and press `Enter`.
- List the disks:
  - Type `list disk` and press `Enter`. This will show you all the `disks` connected to your computer. Identify your `USB Drive` by its size.
- Select the USB disk:
  - Type `select disk #` (replace `#` with the `disk number` of your` USB Drive`) and press `Enter`. For example, if your `USB Drive` is `Disk 1`, type select `disk 1`
- Erase the disk:
  - Type `clean` and press `Enter`. This will `erase all data` and `partitions` on the selected disk.
- Create a primary partition:
  - Type `create partition primary` and press `Enter`.
- Select the partition:
  - Type `select partition 1` and press `Enter`.
- Format the partition as FAT32:
  - Type `format fs=fat32` and press `Enter`. This will format the partition as FAT32.
- Exit DiskPart:
  - Type `exit` and press `Enter` to close DiskPart.

#### Change the label & view the File System using Disk Management of USB Drive

- Open Disk Management:
  - Press `Windows` Key + `R` to open the Run dialog box. Type `diskmgmt.msc` and press `Enter`.
  - Locate the `USB Drive`:
    - In the `Disk Management` window, look for your `USB Drive` in the lower section. It will be listed as `Disk 1` or higher (`Disk 0` is usually your internal drive).
  - Rename & Check the File System of USB Drive:
    - Right-click on `USB Drive`
    - Select `Properties` from the list
    - Go to the `General` tab
    - double click `Drive label` and type ` USB Drive`
    - `Apply`
    - The `File System` is displayed in the `General` tab for the corresponding partition on your `USB Drive`.
    - `OK`

</details>

Next, go to the root of this `USB Drive` and create a folder called `com.apple.recovery.boot`. Then move the downloaded `BaseSystem` or `RecoveryImage` files. Please ensure you copy over both the `.dmg` and `.chunklist` files to [this](https://dortania.github.io/OpenCore-Install-Guide/assets/img/com-recovery.805dc41f.png) folder:

</details>

<details><summary>
    
## 🏗️Adding The Base OpenCore Files
</summary>
    
To setup OpenCore’s folder structure, you’ll want to grab the `EFI` folder found in [OpenCorePkg's releases](https://github.com/acidanthera/OpenCorePkg/releases/). Note that they will be under either the [`X64`](https://dortania.github.io/OpenCore-Install-Guide/assets/img/base-oc-folder.9a1a058a.png) folders, for `64-bit` Firmwares:

> [!NOTE]
> OpenCore-RELEASE.zip: Much snappier boot times, however virtually no useful DEBUG info is provided in OpenCore making troubleshooting much more difficult.

And once downloaded, grab the `EFI` folder inside and place this on the root of the `USB Drive` along side `com.apple.recovery.boot`. Once done it should look like [this](https://dortania.github.io/OpenCore-Install-Guide/assets/img/com-efi-done.a6fb730e.png):

Now lets open up our EFI folder and [see](https://dortania.github.io/OpenCore-Install-Guide/assets/img/base-efi.7500e22d.png) what's inside:

Now something you'll notice is that it comes with a bunch of files in `Drivers` and `Tools` folder, we don't want most of these:

##### Keep the following from Drivers:
Driver|Status|Description
:----|:----|:----
[HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)|Required|Needed for seeing HFS volumes(ie. macOS Installers and Recovery partitions/images)
OpenRuntime.efi|Required|this is needed for proper sleep, shutdown and other services to work correctly
OpenVariableRuntimeDxe.efi|Remove|work with OpenRuntime [...more](https://dortania.github.io/OpenCore-Post-Install/misc/nvram.html#emulating-nvram-with-a-nvram-plist). Only needed for systems without native NVRAM
OpenCanopy.efi|Recommended|`OpenCanopy.efi` is OpenCore bootloader graphical user interface (GUI) Driver. its allows you to use custom themes for your boot screen. You can also customize the icons for each boot entry and change the background image for a more personalized experience.
AudioDxe.efi|Recommended|This Driver used in Hackintosh setups to enable onboard audio functionality to macOS. It's part of the process of recognize and utilize your system's audio hardware.
OpenHfsPlus.efi|Remove| OpenSource version of Apple proprietary HfsPlus.efi driver.
Ext4Dxe.efi|Optional|EXT4 is a Linux file system commonly used in Linux distributions. This driver allows the system to access and mount EXT4-formatted partitions before the operating system (such as Linux or a dual-boot system) is fully loaded.
DpcDxe.efi|Remove(alreadyExist)|Its main purpose is to ensure that DisplayPort devices (like monitors or graphics cards with DisplayPort outputs) are properly initialized and recognized in the pre-boot environment before macOS fully loads its own drivers.
UsbMouseDxe.efi|Optional|its provide support for USB Mice during the early boot stages, particularly when using bootloaders like OpenCore.
OpenUsbKbDxe.efi|Optional|this driver provides a reliable implementation of USB keyboard support in the EFI environment.
ArpDxe.efi|Optional|its provide support ARP (Address Resolution Protocol) functionality during the early stages of booting a Hackintosh. it enables networking support for Ethernet devices before macOS load.
Dhcp4Dxe.efi / Dhcp6Dxe.efi|Optional|it allows the system to obtain an IP address from a DHCP (Dynamic Host Configuration Protocol) server over a network connection (usually Ethernet) before the operating macOS system loads.
DnsDxe.efi|Optional|This driver allows the system to resolve domain names to IP addresses while still in the pre-boot environment (before macOS fully loads). It's particularly useful for network booting or any pre-boot task that requires domain name resolution over a network.
Ip4Dxe.efi / Ip6Dxe.efi|Optional|it enables a UEFI system to communicate over an IPv4 network by implementing basic TCP/IP stack functionality.
SnpDxe.efi|Optional|that provides network support for the System Network Protocol (SNP) in UEFI systems, and it enables network interfaces (such as Ethernet or Wi-Fi) to be used in UEFI environments for tasks like network booting (PXE boot), network configuration, and Internet access during the boot process.
OpenNtfsDxe.efi|Optional|NTFS (New Technology File System) is the default file system used by Windows for its system drive, and it is commonly used for data partitions as well. By using this, OpenCore bootloader can access NTFS drives, which is particularly useful in dual-boot setups where you have both Windows and macOS installed on the same machine.
OpenPartitionDxe.efi|Optional|access and manage partition tables on disks.
FirmwareSettingsEntry.efi|Optional|It allows users to access the UEFI/BIOS setup directly from the OpenCore bootloader, by pressing specific keys (like `F2`, `Delete`, etc.) during the boot process to enter the BIOS settings.
HiiDatabase.efi|Remove(alreadyExist)|HII (Human Interface Infrastructure) is a protocol that allows UEFI firmware to interact with user interfaces and graphical elements during the boot process, including displaying boot menus, settings, and other user interface elements.
ToggleSipEntry.efi|Optional|this tool commonly used in Hackintosh systems to toggle the System Integrity Protection (SIP) on or off from the UEFI.
XhciDxe.efi|Optional|that provides support for the eXtensible Host Controller Interface (XHCI) in a UEFI. XHCI is a standard interface for USB 3.0 and later controllers, and this driver is used to enable USB 3.0 support during the boot process.
NvmExpressDxe.efi|Optional|enable support for NVMe storage devices in a UEFI.
ResetNvramEntry.efi|Recommended|used primarily in Hackintosh setups to manage and reset NVRAM (Non-Volatile Random-Access Memory) entries.
Hash2DxeCrypto.efi|Optional|this driver provides cryptographic hashing functions needed for specific security features, specifically for things like secure boot features.
RngDxe.efi|Optional|a driver that generate a source of random numbers during the boot process, related to `Hash2DxeCrypto.efi` (secure boot).
RamDiskDxe.efi|Optional|a specialized EFI driver for creating and managing RAM disks (a storage volume that resides entirely within the system's RAM) during the boot process. It provides a fast, temporary storage space for use in specialized boot environments.
CrScreenshotDxe.efi|Optional|Used for taking screenshots in UEFI (press `F10` key on your keyboard, the generated screenshot is saved in the root of your `EFI` folder.), not needed by us
Ps2KeyboardDxe.efi + Ps2MouseDxe.efi|Optional|Pretty obvious when you need this, USB keyboard and mouse users don't need it
HttpBootDxe.efi|Optional|It allows a system to boot over the network using an HTTP server to fetch boot files (such as a bootloader or kernel) instead of booting from a local disk or USB drive.
HttpDxe.efi|Optional|It is part of the HTTP Boot feature in UEFI firmware, which allows a system to download and boot files over the network using the HTTP protocol rather than the more common PXE (Preboot Execution Environment) or TFTP (Trivial File Transfer Protocol).
HttpUtilitiesDxe.efi|Optional|It provides utility functions for network booting over the HTTP protocol.
MnpDxe.efi|Optional|This driver allows UEFI firmware to handle Multicast communication over a network interface, facilitating the use of network protocols that rely on multicast, such as certain network booting protocols
TcpDxe.efi|Optional|allowing OpenCore bootloaders to access network resources over TCP (Transmission Control Protocol) or IP. This driver is particularly useful for network booting.
Udp4Dxe.efi / Udp6Dxe.efi|Optional|that provides support for the UDP (User Datagram Protocol) over IPv4 networking in UEFI, which are commonly used for tasks such as network booting.
Mtftp4Dxe.efi / Mtftp6Dxe.efi|Optional|this is a Trivial File Transfer Protocol (TFTP) client driver that allows network booting via the TFTP protocol.
OpenNetworkBoot.efi|Optional|this is a network boot driver designed for more advanced network booting scenarios than basic TFTP.
SnpDxe.efi|Optional|a basic EFI network driver that implements the Simple Network Protocol, related to Network Booting.
TlsDxe.efi|Optional|a EFI driver that implements the Transport Layer Security (TLS) protocol, which allows secure, encrypted network communication, related to Network Booting.
UefiPxeBcDxe.efi|Optional|a driver that enables UEFI systems to boot from a network using the Preboot Execution Environment (PXE) protocol.
BiosVideo.efi|Optional|Fixing Black Screen on Boot phase, related to legacy BIOS.
OpenLegacyBoot.efi|Optional|enable legacy BIOS compatibility during the boot process. Specifically, it allows the UEFI-based system to properly handle legacy booting methods.
OpenLinuxBoot.efi|Optional|It allows a UEFI-based system to boot Linux operating systems, even those that may not have been originally designed with full UEFI compatibility.

##### Keep the following from Tools:
Tool|Status|Description
:----|:----|:----
BootKicker.efi|Optional|BootKicker.efi is a component in bootloader, used to run macOS on non-Apple hardware.
ChipTune.efi|Optional|used to modify boot process by patching firmware
CleanNvram.efi|Optional|it used small amount of memory by the system to store certain settings and variables that need to persist across reboots.
ControlMsrE2.efi|Optional|it used in many modern Intel motherboards to unlocked macOS power management and sleep functions.
CsrUtil.efi|Optional|it's manage macOS System Integrity Protection (SIP) settings. SIP is a security feature in macOS
FontTester.efi|Optional|it's used to font rendering within the OpenCore bootloader. OpenCore uses various graphical elements, including text, to present information and options during the boot process. Ensuring that these fonts render correctly across different resolutions.
GopStop.efi|Optional|it's used to fixed address issues related to the Graphics Output Protocol (GOP) on certain GPUs. The GOP is a component of the UEFI firmware that handles the initialization and output of the graphics card during the boot process.
KeyTester.efi|Optional|its' used to ensure that your keyboard is properly recognized and functioning within the OpenCore bootloader
ListPartitions.efi|Optional|it's used to listing and displaying the partitions present on the system.
MmapDump.efi|Optional|it's used to display the memory map of your system.
OpenControl.efi|Optional|it's allow modify boot config, Providing an interface to interact with hardware components, help troubleshoot hardware or firmware issues.
OpenShell.efi|Recommended|Recommended for easier debugging
ResetSystem.efi|Optional|it's used for resetting the system under various conditions.
RtcRw.efi|Optional|it's used for reading from and writing to the Real-Time Clock (RTC) and modifying RTC-related settings or values.
TpmInfo.efi|Optional|it's provide information about the Trusted Platform Module (TPM) on your system. TPM is a hardware-based security feature that can store cryptographic keys, passwords, and other critical data securely. TPM is used for various security applications, including secure boot, disk encryption, and platform integrity verification.

A cleaned up EFI: look like [this](https://dortania.github.io/OpenCore-Install-Guide/assets/img/clean-efi.10fb2a26.png)

Now you can place your necessary firmware drivers(.efi) into the Drivers folder and Kexts/ACPI into their respective folders. See Gathering Files for more info on which files you should be using.

Here's what a populated EFI can [look](https://dortania.github.io/OpenCore-Install-Guide/assets/img/populated-efi.8d46cc52.png) like (yours will be different):

[OpenCore bootloader graphical user interface (GUI)](https://dortania.github.io/OpenCore-Post-Install/assets/img/gui-nouveau.8ad4a7b4.png):

Add the [Resources folder](https://github.com/acidanthera/OcBinaryData/tree/master/Resources) to `EFI/OC` [look like](https://dortania.github.io/OpenCore-Post-Install/assets/img/folder-gui.e049d147.png)

Reminder:

- `SSDTs` and custom `DSDTs`(`.aml`) go in `ACPI` folder
- `Kexts`(`.kext`) go in `Kexts` folder
- `Firmware drivers`(`.efi`) go in the `Drivers` folder
</details>

<details><summary>
    
## 📥Gathering files
</summary>
    
### Firmware Drivers

Required Drivers (Universal)

- [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi) (Required)

    Needed for seeing HFS volumes(ie. macOS Installers and Recovery partitions/images). Do not mix other HFS drivers
    For Sandy Bridge and older(as well as low end Ivy Bridge(i3 and Celerons), see the legacy section below

- [OpenRuntime.efi](https://github.com/acidanthera/OpenCorePkg/releases) (Required)

    Replacement for `AptioMemoryFix.efi`
    used as an extension for OpenCore to help with patching boot.efi for NVRAM fixes and better memory management.
        Reminder this was bundled in OpenCorePkg we downloaded earlier


### Kexts

Required Kexts(Must haves)

- [Lilu.kext](https://github.com/acidanthera/Lilu/releases) (Required)

    A kext to patch many processes, required for AppleALC, WhateverGreen, VirtualSMC and many other kexts. Without Lilu, they will not work.
    Note that while Lilu supports as early as Mac OS X 10.4, many plugins only work on newer versions.

- [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC/releases) (Required)

  Emulates the SMC chip found on real macs, without this macOS will not boot
        Requires Mac OS X 10.4 or newer
- [SMCProcessor.kext](https://github.com/acidanthera/VirtualSMC/releases) (Recommended) - monitoring CPU temperature, comes with VirtualSMC.kext.

  Used for monitoring CPU temperature, doesn't work on AMD CPU based systems.

- [SMCSuperIO.kext](https://github.com/acidanthera/VirtualSMC/releases) (Recommended) - monitoring fan speed, comes with VirtualSMC.kext.

  Used for monitoring fan speed, doesn't work on AMD CPU based systems.
 
- [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases) (Required)

  Used for graphics patching, DRM fixes, board ID checks, framebuffer fixes, etc; all GPUs benefit from this kext.

- [RadeonSensor.kext](https://github.com/ChefKissInc/RadeonSensor/releases) (Recommended): Used for monitoring GPU temperature on AMD GPU systems. Requires RadeonSensor from the same repository. Requires macOS 11 or newer.

- [AppleALC.kext](https://github.com/acidanthera/AppleALC/releases) (Required) - enable onboard audio.

  Used for AppleHDA patching, allowing support for the majority of on-board sound controllers.

- [NVMeFix.kext](https://github.com/acidanthera/NVMeFix/releases) (Recommended) - for fixing power management and initialization on non-Apple NVMe

- `USBPorts.kext` and `SSDT-UIAC.aml` (Recommended): set port connector types (USB2/3), Required: `SSDT-USBX.aml`, generate using [Hackintool.dmg](https://github.com/benbaker76/Hackintool/releases)

Most used macOS Utilities

Used for fixing dGPU HDMI/DP Audio Volume-Control:

- [Soundflower.dmg](https://github.com/mattingalls/Soundflower/releases): MacOS system extension that allows applications to pass audio to other applications.
- +[SoundflowerBed.pkg](https://github.com/mLupine/SoundflowerBed/releases): SoundflowerBed is an application that resides in the menu bar allowing you to tap into Soundflower channels and route them to an audio device.
- or[BlackHole](https://github.com/ExistentialAudio/BlackHole?tab=readme-ov-file#installation-instructions): modern macOS audio loopback driver that allows applications to pass audio to other applications with zero additional latency, alternative to SoundFlower.

Used for fixing Monitor Display Brightness-Control over dGPU HDMI/DP using monitor Display Data Channel(DDC):

- [MonitorControl.dmg](https://github.com/MonitorControl/MonitorControl/releases) (Recommended): show brighitness/volume slider in mac menu using monitor Display Data Channel/Command Interface(DDC/CI) controller over VGA/HDMI/DP/Type-C.

- [Karabiner-Elements.dmg](https://github.com/pqrs-org/Karabiner-Elements/releases): to fix external Keyboard Scroll Lock & Num Lock on-off function

- [Stats.dmg](https://github.com/exelban/stats/releases) (Recommended): macOS system monitor (CPU utilization, GPU utilization, Memory usage, Disk utilization, Network usage, Fan's control) in your menu bar.

- [OpenRGB.dmg](https://gitlab.com/CalcProgrammer1/OpenRGB/-/releases/) (Recommended): Open source RGB lighting control software.

- [IriunWebcam.dmg](https://iriun.com/) : use your Android/iPhone as a wireless webcam.
 
- [Duet Display.dmg](https://apps.apple.com/us/app/duet-display/id935754064): turns your Android, iPad or iPhone into the most advanced extra display for your Mac & PC.

- [LocalSend.dmg](https://apps.apple.com/us/app/localsend/id1661733229) (Recommended): free, open-source, cross-platform file sharing tool that allows you to share files to nearby devices.

- [Mos.dmg](https://github.com/Caldis/Mos/releases) (Recommended): Reverse the mouse wheel scroll direction.

- [Rectangle.dmg](https://github.com/rxhanson/Rectangle/releases) (Recommended): Move and resize windows on macOS.

+ [QGIS.dmg](https://qgis.org/download/)[GPSD.pkg](https://formulae.brew.sh/formula/gpsd#default): to use USB GPS Receiver for GPSD Maps or other places except Apple Maps.

Other common kexts used on Alder Lake:

- [RestrictEvents.kext](https://github.com/acidanthera/RestrictEvents/releases) (Required) - Lilu Kernel extension for blocking unwanted processes causing compatibility issues on different hardware. - Is needed when enabling E-cores due to large core count and makes showing the proper CPU name possible.

- [CPUFriend.kext](https://github.com/acidanthera/CPUFriend/releases) (Recommended) - A Lilu plug-in for dynamic power management data injection. Used with CpuFriendDataProvider.kext which can be created according to the instructions here: [CPUFriend/Instructions](https://github.com/acidanthera/CPUFriend/blob/master/Instructions.md)

   Partial XCPM compatibility is available, but frequency vector tuning will be [required](https://github.com/dortania/bugtracker/issues/190).

> [!NOTE]
> Power management on non-Apple CPUs can be tricky. If your CPU isn’t being properly managed, it could throttle or not run at optimal speeds, which can result in lag. If you're using an Alder Lake CPU with E-Core, CPUFriend.kext can significantly improve power management and efficiency.

- [AGPM Injector.dmg](https://github.com/Pavo-IM/AGPMInjector/releases): Fixes Apple GPU Power Management settings for desktop GPUs that are supported.

- An Ethernet kext. Commonly found on Z690/Z790/B660/B760:

  [LucyRTL8125Ethernet.kext](https://github.com/Mieze/LucyRTL8125Ethernet/releases) (Recommended) - A macOS driver for Realtek RTL8125 2.5GBit Ethernet Controllers.

- For Intel's 2.5GbE (I225-V) NICs, patches are mentioned in the desktop Alder/Raptor Lake DeviceProperties section. No kext is required.

- [VoodooPS2.kext](https://github.com/acidanthera/VoodooPS2/releases): It provides support for PS/2 input devices, including keyboards, touchpads, and mice, on Hackintosh systems.

- [USBWakeFixup.kext](https://github.com/osy/USBWakeFixup/releases) (Recommended): is needed to fix keyboard wakeup support, but may cause compatibility issues with Bluetooth. Works with `SSDT-USBW`.

- Kexts for USB mapping, depending on the use of [USBToolBox.kext and UTBDefault.kext](https://github.com/USBToolBox/kext/releases) or [USBToolBox.kext](https://github.com/USBToolBox/tool/releases) and USBMap.kext; USBMap Required [Windows.exe](https://github.com/USBToolBox/tool/releases/latest/) or [macOS.py](https://github.com/USBToolBox/tool/archive/refs/heads/master.zip).
  
  <details><summary>
  USB mapping with USBToolBox
  </summary>

  - Download and Extract the [USBToolBox.zip](https://github.com/USBToolBox/tool/releases/latest/) for your Windows 11.
  - Launch the `USBToolBox` by Double click `USBToolBox.exe` in Windows `File EXplorer` > `$env:USERPROFILE\Downloads\USBToolBox\dist\USBToolBox.exe`
  - Select `Discover Ports` by chosing `D` and wait for the listing to populate.
  
  GIGABYTE B660M DS3H AX DDR4 External I/O Connectors:
  - 2 x USB 2.0/1.1 ports
  - 1 x USB 2.0/1.1 ports: Connected Intel(R) Wireless Bluetooth(R) [Intel WiFi 6E AX211 M.2 E]
  - 3 x USB 3.2 Gen 1 ports
  - 1 x USB Type-C port, with USB 3.2 Gen 2 support
   - Internal
     - 1 x USB 2.0/1.1 ports: Connected Intel(R) Wireless Bluetooth(R)
   - Back Panel Connectors:
     - 2 x USB 2.0/1.1 ports
     - 3 x USB 3.2 Gen 1 ports
     - 1 x USB Type-C port, with USB 3.2 Gen 2 support
   
  GIGABYTE B660M DS3H AX DDR4 Internal I/O Connectors
  - 2 x USB 2.0/1.1 headers
  - 1 x USB 3.2 Gen 1 header
  - Internal
    - 2 x USB 2.0/1.1 headers: NotConnected
  - Front Panel Connectors: Connected Case I/O
    - 1 x USB 3.2 Gen 1 header: 
   - Case I/O Ports
     - 2 x USB 3.2 Gen1 Type-A
  
  GIGABYTE B660M DS3H AX DDR4 Total I/O Connectors:
  - 5 x USB 2.0 (2 x Type-A + 2 x USB 2.0 header : NotConnected + 1 x USB 2.0/1.1 ports: Connected Intel(R) Wireless Bluetooth(R))
  - 4 x USB 3.2 Gen 1 Type-A
  - 1 x USB 3.2 Gen 2 Type-C

  - Verify Physical Connections:
   - Connect USB devices to each port individually to confirm port identification. Note which physical ports correspond to the entries USBToolBox lists (Type-A, Type-C, headers, Bluetooth).
  > [!NOTE]
  > you will have to plug in a USB 2 device into each USB 2 port and a USB 3 device into each USB 3 port.
  - for my case:
  ```
  Port 1 | USB 3.0 | USB 3 Type C
   - Cruzer Blade
  Port 2 | USB 3.0 | USB 3 Type A
   - Cruzer Blade
  Port 3 | USB 3.0 | USB 3 Type A
   - Cruzer Blade
  Port 4 | USB 3.0 | USB 3 Type A
   - Cruzer Blade
  Port 5 | USB 2.0 | USB 2.0 Type A
   - USB OPTICAL MOUSE
  Port 6 | USB 2.0 | USB 2.0 Type A
   - Dell KB216 Wired Keyboard
  Port 7 | USB 2.0 | Internal
   - USB2.0 Hub
  Port 9 | USB 3.0 | USB 3 Type A
   - Cruzer Blade
  Port 10 | USB 3.0 | USB 3 Type A
   - Cruzer Blade
  Port 11 | USB 1.1 | Internal
   - ITE Device
  Port 14 | USB 2.0 | Internal
  - Intel(R) Wireless Bluetooth(R)
  ```
  for my case - `Port Discovery` showing i have `26 ports` and macOS has `15-port limit` so, i need to enabled required port includeing: `Port 1`, `Port 2`, `Port 3`, `Port 4`, `Port 5`, `Port 6`, `Port 7`, `Port 9`, `Port 10`, `Port 11`, `Port 14` and disabled others port. so, me_enabled_total_11-port < macOS_has_15-port_limit
  - Select `Back` by chosing `B`
  - 
  - Select `Select Ports and Build Kext` by chosing `S`
    > for my case port 5, 6 are USB 2.0
    ```
    T:5,6:0
    ```
    "USB 2.0 Hub" appearing on Port 7 is a common sight on many motherboards. This usually refers to an internal hub chip that splits a single USB signal from the chipset into multiple internal headers.
    "ITE Device" (RGB Controller or Sensor Chip) appearing on Port 11 is an internal controller on my motherboard. Since it is showing up as USB 1.1, it is not a physical port on my case; rather, it is a specialized chip built into the motherboard.
    ```
    T:7,11,14:255
    ```
    > [!INFO]
    > Even though my Bluetooth (Port 14) is technically a USB 2.0 signal, macOS requires internal devices to be marked as Internal (255) to prevent sleep/wake issues.
  - Enter
    > set custom port name (my port 5, 6 are USB 2.0 Type-A port)
    ```
    C:5,6:USB 2 Type-A
    ```
  - Enter
    > set port 7 name as Internal USB 2 Hub
    ```
    C:7:Internal USB 2 Hub
    ```
    > set port 11 name as Internal ITE Device
    ```
    C:11:Internal ITE Device
    ```
    > set port 14 name as Internal Bluetooth
    ```
    C:14:Internal BT
    ```
  - Enter
    > port 1 type are USB 3.0 Type-C
    ```
    T:1:9
    ```
    ```
    "With Switch" (Type 9)
      Most modern motherboards (especially the ports on the back I/O shield) have a "Switch" (hardware chip: Multiplexer chip).
      Behavior: You plug in a USB-C device, and it works. You flip the cable upside down, plug it back in, and it still works using the same port address (Port 1 in my case).
      Mapping: Because the hardware chip handles the "flip," macOS only sees one logical port. That is why we use Type 9.
    "Without Switch" (Type 10)
      Some cheaper motherboards or front-panel Type-C headers do not have a "Switch" (hardware chip: Multiplexer chip).
      Behavior: If you plug the cable in one way, it shows up as Port 1. If you flip the cable, it shows up as a different port number (e.g., Port 2).
      Mapping: In this case, macOS sees two separate "half-ports." You have to set both of those port numbers to Type 10.
    ```
    > port 1, 2, 3, 4, 9, 10 type are USB 3.0
    ```
    T:2,3,4,9,10:3
    ```
    > [!INFO]
    > Ports 9 and 10 are standard USB 3.0 ports (connected via the 19-pin internal header to my computer cabinet/chassis)
  - Enter
    > set port 2, 3, 4, 9, 10 name as USB 3.0 Type-A
    ```
    C:2,3,4,9,10:USB 3 Type-A
    ```
  - Enter
    > give port 1 name as USB 3.0 Type-C
    ```
    C:1:USB 3 Type-C
    ```
  - Enter
   ```
   Port 1 | USB 3.0 | USB 3 Type C
   USB 3 Type-C
    - Cruzer Blade

   Port 2 | USB 3.0 | USB 3 Type A
   USB 3 Type-A
    - Cruzer Blade

   Port 3 | USB 3.0 | USB 3 Type A
   USB 3 Type-A
    - Cruzer Blade

   Port 4 | USB 3.0 | USB 3 Type A
   USB 3 Type-A
    - Cruzer Blade

   Port 5 | USB 2.0 | USB 2 Type A
   USB 2 Type-A
    - USB OPTICAL MOUSE

   Port 6 | USB 2.0 | USB 2 Type A
   USB 2 Type-A
    - Dell KB216 Wired Keyboard

   Port 7 | USB 2.0 | Internal
   Internal USB 2 Hub
    - USB2.0 Hub

   Port 9 | USB 3.0 | USB 3 Type A
   USB 3 Type-A
    - Cruzer Blade

   Port 10 | USB 3.0 | USB 3 Type A
   USB 3 Type-A
    - Cruzer Blade

   Port 11 | USB 1.1 | Internal
   Internal ITE Device
    - ITE Device

   Port 14 | USB 2.0 | Internal
   Internal BT
    - Intel(R) Wireless Bluetooth(R)
   ```
   > [!NOTE]
   > Sometimes, a `USB 3.0 port` will default to` USB 2.0` if a `USB 2.0 device` was connected to `USB 3.0 port` when the USBMap was created. Try testing the `USB 3.0 ports` with a `USB 3.0 device` (like a `USB 3.0 flash drive`) & `USB 2.0 ports` with a `USB 2.0 device` (like a `USB 2.0 flash drive`) to ensure USBToolBOx & macOS recognizes the 2.0 port as 2.0 and 3.0 as 3.0. especially since dual-role ports (with both `USB 2.0` and `USB 3.0` capabilities) can sometimes default to `USB 2.0`.
  - Select `Enable All Populated Ports` by chosing `P` (`populated port` means `port with a connected device`)
  - Enter
  - Select `Disable All Empty Ports` by chosing `D`
  - Enter
  - select "Build UTBMap.kext (requires [USBToolBox.kext](https://github.com/USBToolBox/kext/releases))" by chosing `K`
  - Enter
  - `Close` USBToolBox PowerShell window or chose `B` then chose `B` then enter `Q`.

  copy Generate `USBMap.kext` & Download `USBToolBox.kext` into `EFI/OC/Kexts`:

  - now Copy this `USBMap.kext` file into `EFI/OC/Kexts` on your OpenCore `EFI` partition from `C:\Users\user_name\Downloads\Windows\dist\UTBMap.kext`.
  - also Download, Extract and Copy [USBToolBox.kext](https://github.com/USBToolBox/kext/releases) file into `EFI/OC/Kexts` on your OpenCore `EFI` partition. (requires)

  </details>

- [USBInjectAll.kext](https://github.com/daliansky/OS-X-USB-Inject-All/releases) (only Recommended if you dont Map USB Port): Used for injecting Intel USB controllers on systems without defined USB ports in ACPI.
All Intel chipset series.
Requires OS X 10.11 or newer.

> [!NOTE]
> if you are map your USB Port and using USBToolBox don't use USBInjectAll.kext its conflict with USBToolBox.kext+USBMap.kext and you get OpenCore boot error.

- [FeatureUnlock.kext](https://github.com/acidanthera/FeatureUnlock/releases) (Recommended): Add Sidecar, NightShift, AirPlay, Universal Control and Continuity Camera support.

- [HoRNDIS.pkg](https://github.com/jwise/HoRNDIS): Android USB tethering driver for Mac OS X
  - [HoRNDIS.kext](https://github.com/Edwardwich/HoRNDIS/releases) (Recommended)

- [WirelessUSBAdapter.kext](https://github.com/chris1111/Wireless-USB-Big-Sur-Adapter): [see](https://github.com/chris1111/Wireless-USB-Big-Sur-Adapter?tab=readme-ov-file#support-drivers-adapter) supported Wireless USB Adapter list (ie. TPLink Archer T2U NANO, DLink DWA131E 92EU, Realtek RTL8812BU).

- [MediatekWiFi.kext](https://github.com/chris1111/D-LinkUtility-Package/releases): MediatekWiFi.kext for MT7601, MT7610, MT7621U.

- [RealtekWiFi.kext](https://github.com/chris1111/Wireless-USB-Big-Sur-Adapter/releases): [see](https://github.com/chris1111/Wireless-USB-Big-Sur-Adapter?tab=readme-ov-file#support-drivers-adapter) supported Realtek WiFi chipset list (ie. RTL8811AU, RTL8812AU, RTL8812BU, RTL8812AU-VL, RTL8812AU-VN, RTL8812AU-VS, RTL8814AU)

  
intel WiFi and Bluetooth kext:

- [AirportItlwm.kext / itlwm.kext](https://github.com/OpenIntelWireless/itlwm/releases) (Recommended): Adds support for a large variety of INTEL WIRELESS cards and works natively in recovery
- +[HeliPort.dmg](https://github.com/OpenIntelWireless/HeliPort/releases) (Recommended): Intel WiFi Client for `itlwm`

> [!NOTE]
> Don't enable both `Airportitlwm.kext` & `Itlwm.kext`. If you want to have [iMessage](https://apps.apple.com/us/app/messages/id1146560473), [FaceTime](https://apps.apple.com/us/app/facetime/id1110145091) working, then use `Itwlm.kext`. But during macOS install you need to use `Airportitlw.kext` to get WiFi internet. If you are using `Itlwm.kext` you will need `HeliPort.dmg` app to connect to WiFi.

- [IntelBluetoothFirmware.kext + IntelBTPatcher.kext](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/releases) (Recommended): Adds Bluetooth support to macOS when paired with an Intel wireless card.
- +[BlueToolFixup.kext](https://github.com/acidanthera/BrcmPatchRAM/releases) (Recommended): that comes with BrcmPatchRAM kexts.

- [intel WiFi 7 kext](https://github.com/OpenIntelWireless/itlwm/issues/955#issuecomment-2133764652) (Recommended): for Intel BE200 / BE201

Broadcom WiFi and Bluetooth kext:

- [AirportBrcmFixup.kext](https://github.com/acidanthera/AirportBrcmFixup/releases):
Used for patching non-Apple/non-Fenvi Broadcom cards

- [BrcmPatchRAM.kext](https://github.com/acidanthera/BrcmPatchRAM/releases):
Used for uploading firmware on Broadcom Bluetooth chipset, required for all non-Apple/non-Fenvi Airport cards.

P-cores and E-cores kext:

- [CpuTopologyRebuild.kext](https://github.com/b00t0x/CpuTopologyRebuild/releases) (Recommended): An experimental Lilu plugin that optimizes Alder Lake's heterogeneous core configuration. Only for Alder/Raptor Lake CPUs.
> [!IMPORTANT]
> Make sure to use `CpuTopologyRebuild.kext`. This lets Intel's heterogenous architecture (E-/P-cores) be used more optimally; macOS, by default, can't tell the difference between E-Cores and P-cores, since no real Macs use this architecture. I would recommend using it with the `-ctrsmt` boot arg, which makes MacOS see the E-cores as additional SMT threads, rather than as independent cores. Otherwise, the greater number of E-cores means macOS would be > more likely to send heavier threads to them than are optimal for them to manage.

> Install it like any other kext. Add bootflag like any other bootflag. Make sure `ProvideCurrentCpuInfo` under Quirk is `Enabled`! 

Navi 22 (ie. RX 6700 XT, RX 6750 XT) Specific Kext:

- [NootRX.kext](https://github.com/ChefKissInc/NootRX/) (Recommended): to use this kext, remove `WhateverGreen.kext`
</details>

<details><summary>

## 🔪Alder / Raptor Lake SSDTs
</summary>

SSDT (Secondary System Description Table) that defines EC (Embedded Controller) settings. It is part of the configuration that is required to ensure macOS can properly interact with the system's embedded controller, which is responsible for controlling things like power management, battery monitoring, thermal management, and other system-level functions on desktops.

SSDTs|Description|Download
:----|:----|:----
★SSDT-HPET|Patches out IRQ conflicts|Prebuilt \| [Atomated](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#running-ssdttime--atomated) \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#ssdts-the-manualy)
★SSDT-EC|Embedded Controller (EC) is a small, low-level microcontroller that manages critical functions, such as keyboard input, fan control, and charging.|Prebuilt \| [Atomated](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#running-ssdttime--atomated) \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#ssdts-the-manualy)
☆SSDT-EC-USBX|SSDT that deals with USB Extended (USBX) configurations in relation to the EC. It is a specific type of SSDT used to improve USB port functionality, particularly for where USB ports and EC management need to be harmonized for macOS to properly detect and manage USB devices.|[Prebuilt](https://github.com/dortania/Getting-Started-With-ACPI/raw/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml) \| [Atomated](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#running-ssdttime--atomated) \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#ssdts-the-manualy)
★SSDT-PLUG-ALT|Allow the kernel's XCPM (XNU's CPU Power Management) to manage Alder Lake and newer CPU's power management. its fixes potential issues such as sleep/wake function and improves CPU performance|[Prebuilt](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml) \| [Atomated](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#running-ssdttime--atomated) \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#ssdts-the-manualy)
★SSDT-RTCAWAC|custom SSDT designed to modify or correct the RTC (Real-Time Clock) and its associated ACPI (Advanced Configuration and Power Interface) settings. Specifically, RTCAWAC is intended to address issues with RTC Wake-from-AC (Wake After Sleep or Waking after powering down) functions in Hackintosh systems|[Prebuilt](https://github.com/dortania/Getting-Started-With-ACPI/raw/master/extra-files/compiled/SSDT-AWAC.aml) \| [Atomated](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#running-ssdttime--atomated) \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#ssdts-the-manualy)
SSDT-RHUB|certain OEMs (ie. Asus) have broken the ACPI spec and this results in issues when booting into macOS. To fix this, we'll want to turn off the RHUB device and force macOS to manually rebuild the ports.|[Prebuilt](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-RHUB.aml) \| [Atomated](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#running-ssdttime--atomated) \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#ssdts-the-manualy)
SSDT-Bridge|to Correct Unnamed PCI Bridges. This is needed if you have to spoof a GPU with unnamed PCI bridges. ie. `Radeon RX 6950 XT`|Prebuilt \| [Atomated](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#running-ssdttime--atomated) \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#from-windows)
SSDT-DMAR|to Fix `Intel I225` & Aquantia (ie. `AQC113C`/ `AQC113`/ `AQC107`) based Ethernet Controllers connection becomes unstable.| Prebuilt \| [Atomated](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#running-ssdttime--atomated) \| [Manual](https://dortania.github.io/Getting-Started-With-ACPI/Universal/dmar-methods/manual.html)
SSDT-SBUS-MCHC|handles the System Management Bus by fixing AppleSMBus support, which has many functions like: AppleSMBusController - Aids with correct temperature, fan, voltage, ICH, etc readings, AppleSMBusPCI - Same idea as AppleSMBusController except for low bandwidth PCI devices, Memory Reporting - Aids in proper memory reporting and can aid in getting better kernel panic details if memory related.|Prebuilt \| [Atomated](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#running-ssdttime--atomated) \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#ssdts-the-manualy)
SSDT-USBW|Fix a certain USB wakeup issue on OSX, work with [USBWakeFixup.kext](https://github.com/osy/USBWakeFixup/releases)| Prebuilt \| Atomated \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#ssdt-usbwmanualy)
☆SSDT-DMAC|Alder/ Raptor Lake motherboards often do not include a `PNP0200` Direct Memory Access Controller (DMAC) Controller, which macOS expects. SSDT-DMAC fixes this by adding a virtual DMA controller. It helps avoid boot issues or ACPI errors related to missing DMAC.| Prebuilt \| Atomated \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#ssdt-dmacmanualy)
SSDT-GPU-SPOOF|mainly needed for dGPUs that are not natively supported| Prebuilt \| Atomated \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#renaming-gpus-ssdt-gpu-spoof)
Spoof-SSDT|Disabling specific dGPU| Prebuilt \| Atomated \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#from-windows)
SSDT-DTPG|Related to Thunderbolt| Prebuilt \| Atomated \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#from-windows)
SSDT-UIAC|set port connector types (USB2/3), work with `SSDT-USBX`, `USBPorts.kext`. you can generate it usng [Hackintool.dmg](https://github.com/benbaker76/Hackintool/releases)| Prebuilt \| Atomated \| [Manual](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#%EF%B8%8Fusb-fixes-by-usb-mapping)

> ★ mark are required

### SSDTs: The easy way

So here we'll be using a super simple tool made by CorpNewt: [SSDTTime](https://github.com/corpnewt/SSDTTime)

What this tool does is, it dumps your DSDT from your firmware, and then creates SSDTs based off your DSDT. This must be done on the target machine running either Windows

#### Running SSDTTime  (Atomated)

Run the `SSDTTime.bat` file as Admin on the target machine and you should [see](https://dortania.github.io/Getting-Started-With-ACPI/assets/img/ssdttime.0bc50ec0.png) something like this:

##### What are all these options?:

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
P. `Dump DSDT` - Automatically dump the system DSDT
   - Dumps your DSDT from your firmware
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   1. `FixHPET` - Patch out IRQ Conflicts
      - `IRQ` patching, mainly needed for X79, X99 and laptop users(use option C to omit conflicting legacy IRQs)

   2. `FakeEC` - OS-aware Fake EC
      - This is the `SSDT-EC`, required for Catalina and newer users
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   4. `USBX` - Power properties for USB on SKL and newer SMBIOS
      - This is the `SSDT-USBX`. The prebuilt version can be used if desired, but SSDTTime can build a customizable version of SSDT-USBX.

   5. `PluginType` - Sets plugin-type = 1 on First ProcessorObj
      - This is the `SSDT-PLUG`, and can be used on Haswell and newer. Will also check and redefine processor objects for 12th generation and newer Intel systems.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   7. `RTCAWAC` - Context-Aware AWAC Disable and RTC Enable/Fake/Range Fix
      - This is the `SSDT-AWAC/RTC0`, its purpose is to fix the system clocks found on newer hardware, and also enable, fake, and/or fix the RTC range.

   8. `USB Reset` - Reset USB controllers to allow hardware mapping
      - This is `SSDT-RHUB`, used for resetting USB ports in macOS for Asus's Z490 motherboards

   9. `PCI Bridge` - Create missing PCI bridges for passed device path
      - This will create missing PCI bridges necessary for passing device path.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   B. `Fix DMAR` - Remove Reserved Memory Regions from the DMAR Table
      - This is primarily needed for devices that require VT-d functionality such as: `Intel I225` based ethernet controllers, Aquantia (ie. `AQC113C`/`AQC113`/`AQC107`) Ethernet Controllers and some WiFi Devices.

   C. `SMBus` - Defines an `MCHC` and BUS0 device for SMBus compatibility

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
> we want to do is select option `P. Dump DSDT` first, then select the appropriate option(s) for your system.

#### Adding to OpenCore

##### Manual Method

Don't forget that SSDTs need to be added to OpenCore, reminder that `.aml` is compiled, `.dsl` is code. Add only the `.aml` file:

`EFI/OC/ACPI` from "$env:USERPROFILE\Downloads\SSDTTime-master\Results"
`config.plist` -> `ACPI` -> `Add`
Reminder that `Cmd/Ctrl+R` with ProperTree pointed at your `OC` folder will add all your `SSDTs`, `kexts` and `.efi drivers` to the config for you.

#### SSDTs: The Manualy

##### SSDT-USBW	Manualy
Fix a certain USB wakeup issue.

- Find USB Controller ACPI Paths using Device Manager in Windows:
  - Opne Windows `Device Manager`
    - right click on `Windows` icon
    - select `Device Manager`.
  - Identify `USB Controllers`
    Look for entries such as:
    - `Intel(R) USB 3.0 eXtensible Host Controller`
    - for my case: `Intel(R) USB 3.20 eXtensible Host Controller - 1.20 (Microsoft)`
  - Extract USB Controller `ACPI Path`
    - Right-click on a `USB controller` and select `Properties`.
    - Go to the `Details` tab.
    - Select `Location Paths` from the dropdown.
    - for my case: `ACPI(_SB_)#ACPI(PC00)#ACPI(XHCI)`
    - for my case: final `ACPI Path` is - `\_SB.PC00.XHCI`
> converting a file path in a hierarchical file system. The `#` symbols act as separators between levels in the ACPI namespace, and they are replaced with dots `(.)` to form the final path.

- Updated [SSDT-USBW.dsl](https://github.com/osy/USBWakeFixup/blob/master/SSDT-USBW.dsl) Template
Here’s the corrected SSDT with my USB controller's Path:
```dsl
/**
 * USB wakeup virtual device
 */
DefinitionBlock ("", "SSDT", 2, "OSY86 ", "USBW", 0x00001000)
{
    External (\_SB.PC00.XHCI._PRW, MethodObj)

    // We only enable the device for OSX
    If (CondRefOf (\_OSI, Local0) && _OSI ("Darwin"))
    {
        Device (\_SB.USBW)
        {
            Name (_HID, "PNP0D10")  // _HID: Hardware ID
            Name (_UID, "WAKE")  // _UID: Unique ID

            Method (_PRW, 0, NotSerialized)  // _PRW: Power Resources for Wake
            {
                Return (\_SB.PC00.XHCI._PRW ()) // Replace with path to your USB device
            }
        }
    }
}
```
> in both the `External (_SB.PCI0.XHC._PRW, MethodObj)` and `Return (\_SB.PC00.XHC._PRW ())`: This line declares that the `_PRW` method (Power Resources for Wake) of your XHC (eXtensible Host Controller) device is defined elsewhere. This is the method that provides information about the power resources required for USB wakeup.

> You need to replace `_SB.PCI0.XHC` with the correct `ACPI Path` to your `XHC controller`, which in my case is `_SB.PC00.XHCI`.

> `Method (_PRW)` :  Leave the GPE number `(0x0D)` and wake capability `(0x04)` as they are unless specific debugging reveals issues. These values are standard for most systems.

- Compile the `.dsl` file into `.aml` using [SSDTTime](https://github.com/corpnewt/SSDTTime)

```
path/to/iasl.exe path/to/SSDT-USBW.dsl
```

- Add the compiled SSDT-USBW.aml to your OpenCore:
  - Place it in under `EFI/OC/ACPI/Add` to config.plist

##### SSDT-DMAC	Manualy

It helps avoid boot issues or ACPI errors related to missing DMAC.

Check ACPI Path Using Windows Device Manager

Open Device Manager: Press `Win + X` and select `Device Manager`.

Find the PCI Bus: Expand `System Devices` > `Other devices` > Look for `Intel SMBus` Controller or similar entries.

Check ACPI Path: Right-click `Intel SMBus` Controller → `Properties` → Go to `Details` → From the `Property` dropdown, select `Location paths`.

Look Second Value of `Location paths` It should show something like: `_SB.PC00`

> Note: it’s usually mapped to `_SB.PC00` or `_SB.PCI0`.

SSDT-DMAC.dsl
```dsl
/*
 * SSDT-DMAC for Alder Lake and Raptor Lake Hackintosh
 * Enables the missing Direct Memory Access Controller
 */

DefinitionBlock ("", "SSDT", 2, "ACDT", "DMAC", 0x00000000)
{
    External (_SB_.PC00, DeviceObj)

    Scope (\_SB.PC00)
    {
        Device (DMAC)
        {
            Name (_HID, EisaId ("PNP0200"))  // Hardware ID
            Name (_UID, 0)                  // Unique ID
        }
    }
}
```

> Note: Name (_HID, EisaId ("PNP0200")) does not need to change. This value must remain "PNP0200" because it represents the legacy Direct Memory Access Controller (DMAC) that macOS expects.

For `_SB.PC00` systems: ✅ Use Scope `(\_SB.PC00)`, ✅ Use External `(\_SB.PC00)`.

For `_SB.PCI0` systems: ✅ Use Scope `(\_SB.PCI0)`, ✅ Use External `(\_SB.PCI0)`.

- Compile the `.dsl` file into `.aml` using [SSDTTime](https://github.com/corpnewt/SSDTTime)

```
path/to/iasl.exe path/to/SSDT-DMAC.dsl
```

- Add the compiled `SSDT-DMAC.aml` to your OpenCore:
  - Place it in under `EFI/OC/ACPI/Add` to config.plist

<details><summary>
SSDT-DTPG Manualy
</summary>

Related to Thunderbolt
- Identify the Thunderbolt PCI Path 
  - Use Device Manager:
    - Opne Windows `Device Manager`
    - Look for entries related to Thunderbolt. The typical device names might be `Thunderbolt Controller`, `TBT`, or similar.
    - right click `Thunderbolt` decice name
    - `Properties`
    - `Details` tab
    - `Location paths`
    - Note the PCI Path (e.g. `\_SB.PCI0.RP05`)

> For the `Asus ProArt Z790 Creator WiFi`, the most likely paths are: `\_SB.PCI0.RP05`

- Create the SSDT-DTPG.dsl (.asl)

```asl
DefinitionBlock ("", "SSDT", 2, "Hackintosh", "DTPG", 0x00000000)
{
    External (_SB_.PCI0.RP05, DeviceObj)

    Scope (\_SB.PCI0.RP05)
    {
        Method (_DSM, 4, NotSerialized)
        {
            If (Arg2 == Zero) { Return (Buffer() { 0x03 }) }
            Return (Package()
            {
                "compatible", Buffer() { "pci-thunderbolt" },
                "device-id", Buffer() { 0x12, 0x34, 0x56, 0x78 },
                "Thunderbolt native-mode", Buffer() { 0x01 }
            })
        }
    }
}
```

> Replace `RP05` with the actual PCI Path of your Thunderbolt controller if different. RootPath(RP)

- Important Notes:
  - The `PCI Path` is unique to your hardware configuration. Using the wrong Path will result in macOS not recognizing the Thunderbolt controller.
  - The `"pci-thunderbolt"` property is fixed and universal for Thunderbolt injection in macOS. It does not need customization.

- Save the above code as `SSDT-DTPG.dsl`.

- Compile the SSDT-DTPG.dsl

  - Compile it into `.aml` using iasl
    ```
    path/to/iasl.exe path/to/SSDT-DTPG.dsl
    ```

- Add the SSDT to OpenCore

  - Copy `SSDT-DTPG.aml` to your OpenCore EFI folder: `EFI/OC/ACPI/`.
  - `SSDT-DTPG.aml` = True in config.plist -> `ACPI` > `Add`

- BIOS Configuration for Thunderbolt
Ensure the following settings are configured in your Motherboard BIOS:
  - `Thunderbolt Support` = `Enabled`.
  - `Thunderbolt Boot Support` = `Enabled`.
  - `Security Level` = `No Security` (or appropriate level for your use case).
  - `Native OS Support` = `Enabled` (if present).

</details>

<details><summary>
SSDT-Bride Manualy using SSDTTime
</summary>

to Correct dGPU Unnamed PCI Bridges.
    
- Find dGPU PCI Path:
  - Open Windows `Device Manager`
  - right click `Radeon RX xxxx Series` under `Display adapters` in `Device Manager`
  - `Properties`
  - go to `Details` tab
  - select `Location paths` form `Property` dropdown menu
  - Note your `PCI` Value (for `Radeon RX 6950 XT`: `PCIROOT(0)#PCI(0100)#PCI(0000)#PCI(0000)#PCI(0000)`)
    - so `Radeon RX 6950 XT` Final `PCI Path`: `PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)`
  - Note your `ACPI` Value (for `Radeon RX 6950 XT`: `ACPI(_SB_)#ACPI(PC00)#ACPI(PEG1)#ACPI(PEGP)#PCI(0000)#PCI(0000)`)
    - The `ACPI Path` starts out with named bridges `PC00, PEG1, PEGP,` but then at the end we have 2 unnamed bridges `#PCI(0000)#PCI(0000)`. This is why we need `SSDT - Bridge`.
- Generate SSDT-Bride:
  - Go back to [SSDTTime](https://github.com/corpnewt/SSDTTime) main windows. select `PCI Bridge` by Choosing option `9`.
    - You should see: `Please enter the device path needing bridges:`
  - Here you just copy and paste dGPU Final PCI Path `PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)` to the SSDTTime terminal and hit `Enter`.
  - You will end up with `SSDT-Bridge.aml` and `SSDT-Bridge.dsl` in your `C:\Users\user\Downloads\SSDTTime-master\Results` folder.
  - Copy `SSDT-Bridge.aml` file to your OpenCore `EFI > OC > ACPI` folder.
- Customize dGPU Bridge name (Optional):
  - Open `SSDT-Bridge.dsl` in a text editor ([Visual Studio Code](https://apps.microsoft.com/detail/XP9KHM4BK9FZ7Q) or Notepad) from your `C:\Users\user\Downloads\SSDTTime-master\Results` folder.
  - it should looked like this:
```dsl
DefinitionBlock ("", "SSDT", 2, "CORP", "PCIBRG", 0x00000000)
{
    /*
     * Start copying here if you're adding this info to an existing SSDT-Bridge!
     */
    External (\_SB.PC00.PEG1.PEGP, DeviceObj)
    Scope (\_SB.PC00.PEG1.PEGP)
    {
        Device (BRG0)
        {
            Name (_ADR, Zero)
            // Customize this device name if needed, eg. GFX0
            Device (PXSX)
            {
                // Target Device Path:
                // PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)
                Name (_ADR, Zero)
            }
        }
    }

    /*
     * End copying here if you're adding this info to an existing SSDT-Bridge!
     */

}    
```

Here there's a couple things to change:

```
Device (PXSX)
```

For our example, we'll change all mentions of :

```
PXSX with GFX0
```
   - after change `Save` this file.
   - compile this file into `aml` using `isl.exe`:
     ```
     $env:USERPROFILE\Downloads\SSDTTime-master\Scripts\isl.exe $env:USERPROFILE\Downloads\SSDTTime-master\Results\SSDT-Bridge.dsl
     ```
   - You will end up with `SSDT-Bridge.aml` in your `$env:USERPROFILE\Downloads\SSDTTime-master\Results` folder.
   - Copy `SSDT-Bridge.aml` file to your OpenCore `EFI > OC > ACPI` folder.
</details>

<details><summary>
Spoof-SSDT Manualy
</summary>

Disabling specific dGPU using SSDT:

There are many ways to find the path but generally, the easiest way is to get into `Device Manager` under windows and find the `APCI Path`.

Example of device path for `\_SB.PCI0.PEG0.PEGP`:

```dsl
DefinitionBlock ("", "SSDT", 2, "DRTNIA", "spoof", 0x00000000)
    {
       External (_SB_.PCI0.PEG0.PEGP, DeviceObj)

       Method (_SB.PCI0.PEG0.PEGP._DSM, 4, NotSerialized)
       {
          If ((!Arg2 || !(_OSI ("Darwin"))))
          {
             Return (Buffer (One)
             {
                0x03
             })
          }

          Return (Package (0x0A)
          {
             "name",
             Buffer (0x09)
             {
                "#display"
             },

             "IOName",
             "#display",
             "class-code",
             Buffer (0x04)
             {
                0xFF, 0xFF, 0xFF, 0xFF
             },
          })
       }
    }
```

A copy of this SSDT can be found here: [Spoof-SSDT.dsl](https://github.com/dortania/OpenCore-Install-Guide/blob/master/extra-files/Spoof-SSDT.dsl). You will need [SSDTTime](https://github.com/corpnewt/SSDTTime) to compile this. Remember that `.aml` is assembled and `.dsl` is source code. You can compile with `iasl.exe` by Open PowerShell & Enter following commands:

```
path/to/iasl.exe path/to/Spoof-SSDT.dsl
```

add result `Spoof-SSDT.aml` file to OpenCore `EFI > OC > ACPI` folder.

Enabled `Spoof-SSDT.aml` in your config.plist `Root > ACPI > Add`

ACPI|Type|Value|Path
:----|:----|:----|:----
Path|String|Spoof-SSDT.aml|Root > ACPI > Add
Enabled|Boolean|True|
</details>

##### From Windows

- [SSDTTime](https://github.com/corpnewt/SSDTTime)

Supports Windows for DSDT dumping

8. Dump DSDT - Automatically dump the system DSDT

- [acpidump.exe](https://acpica.org/downloads/binary-tools)

- [SSDTs.dsl](https://github.com/dortania/Getting-Started-With-ACPI/tree/master/extra-files/decompiled)

In command prompt run 
```
path/to/acpidump.exe path/to/SSDT.dsl
```
this will dump your SSDT as a .dat file. Rename this to SSDT.aml

#### [Manualy Patching DMAR Table](https://dortania.github.io/Getting-Started-With-ACPI/Universal/dmar-methods/manual.html#preparation): is necessary for Intel I225 based & Aquantia Ethernet Controllers (ie. AQC113C/AQC113/AQC107)

## 🤕Renaming GPUs (SSDT-GPU-SPOOF)

So this is mainly needed for GPUs that are not natively supported out of the box due to their names, most commonly:

- AMD Radeon RX 550 (Lexa Core)
- AMD Radeon RX 6900XTXH (Navi 21)
- AMD Radeon RX 6950 XT (Navi 21)
- AMD Radeon RX 6650 XT (Navi 23)

to spoof the GPU, we need to find a couple things:

- Suitable PCI ID for the GPU
- ACPI Path of the GPU
- [SSDT-GPU-SPOOF.dsl](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/decompiled/SSDT-GPU-SPOOF.dsl.zip)


### [Finding a suitable PCI ID using Web](https://pci-ids.ucw.cz/read/PC/1002):
To find a suitable PCI ID, we'll be using [PCI ID Repository](https://pci-ids.ucw.cz/read/PC/1002) which has a full database of all AMD GPUs. For this example, we'll be creating a Spoof SSDT for the AMD Radeon RX 550. For a full list of supported GPUs, please see the [GPU Buyers Guide](https://dortania.github.io/GPU-Buyers-Guide/).

[PCI ID for Radeon RX 550](https://admin.pci-ids.ucw.cz/read/PC/1002/67ff)


```
Vendor 1002 -> Device 1002:67ff
```

Now lets break this down into a device ID we can use:

```
    1002: The vendor ID, all AMD devices have this ID
    67FF: The device ID, this is what we care about
```

So how do we convert this to a fake ID? Well the format of a fake ID:

```dsl
"device-id",
Buffer (0x04)
{
     0xFF, 0x67, 0x00, 0x00
},
```

### [Finding ACPI Path of the GPU](https://dortania.github.io/Getting-Started-With-ACPI/Universal/spoof.html#finding-the-acpi-path-of-the-gpu)

Windows

To find the PCI path of a GPU is fairly simple, best way to find it is running Windows:

   - Open Device Manager
   - Select Display Adapters, then right click your GPU and select Properties
   - Under the Details Tab, search for `Location Paths`
        Note some GPUs may be hiding under "BIOS device name"

i am using `AMD Radeon RX 550 4GB GDDR5 (Lexa)` for my case:

Radeon RX 550 Properties ─ Details
                           
                            └── Location Paths
                           
                            ├── PCI Path: PciRoot(0)#Pci(0100)#Pci(0000)
                           
                            └── ACPI Path: ACPI(_SB_)#ACPI(PC00)#ACPI(PEG1)#ACPI(PEGP_)

Radeon RX 550 ─ Final Paths
                
                  ├── PCI Path: PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)
                
                  └── ACPI Path: \_SB.PC00.PEG1.PEGP

@another example:

Radeon RX 6950 XT ─ Final Paths
                
                  ├── PCI Path: PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)
                
                  └── ACPI Path: \_SB.PCI0.GPP8.SWUS.SWDS.VGA

@another example:

Radeon RX 6650 XT ─ Final Paths
                
                  ├── PCI Path: PciRoot(0x0)/Pci(0x3,0x1)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)
                
                  └── ACPI Path: \_SB.PCI0.GPP8.PBR0.GFX1.GFX0

### Making the SSDT

so AMD Radeon RX 550 final SSDT-GPU-SPOOF.dsl is: 

```dsl
// Based off of WhateverGreen's sample.dsl
// https://github.com/acidanthera/WhateverGreen/blob/master/Manual/Sample.dsl
DefinitionBlock ("", "SSDT", 2, "DRTNIA", "AMDGPU", 0x00001000)
{
    External (_SB_.PC00, DeviceObj)
    External (_SB_.PC00.PEG1.PEGP, DeviceObj)


    Scope (\_SB_.PC00.PEG1.PEGP)
    {
        if (_OSI ("Darwin"))
        {
            Method (_DSM, 4, NotSerialized)  // _DSM: Device-Specific Method
            {
                Local0 = Package (0x04)
                {
                    // Where we shove our FakeID
                    "device-id",
                    Buffer (0x04)
                    {
                        0xFF, 0x67, 0x00, 0x00
                    },

                    // Changing the name of the GPU reported, mainly cosmetic
                    "model",
                    Buffer ()
                    {
                        "AMD Radeon RX 550"
                    }
                }
                DTGP (Arg0, Arg1, Arg2, Arg3, RefOf (Local0))
                Return (Local0)
            }
        }
    }
    Scope (\_SB.PC00)
    {                   
        Method (DTGP, 5, NotSerialized)
        {
            If (LEqual (Arg0, ToUUID ("a0b5b7c6-1318-441c-b0c9-fe695eaf949b")))
            {
                If (LEqual (Arg1, One))
                {
                    If (LEqual (Arg2, Zero))
                    {
                        Store (Buffer (One)
                            {
                                 0x03
                            }, Arg4)
                        Return (One)
                    }

                    If (LEqual (Arg2, One))
                    {
                        Return (One)
                    }
                }
            }

            Store (Buffer (One)
                {
                     0x00
                }, Arg4)
            Return (Zero)
        }
      
    }

}
```

Here there's a couple things to change:

```
External (_SB_.PCI0, DeviceObj)
External (_SB_.PCI0.PEG0.PEGP, DeviceObj)
```

For our example, we'll change all mentions of :

```
    PCI0 with PC00
    PEG0 with PEG1
```

Hint: If your ACPI path is a bit shorter than the example, this is fine. Just make sure the ACPI paths are correct to your device.

Now that the ACPI pathing is correct, we can finally apply our fake ID!!!

So the 2 parts we want to change:

device ID:

```dsl
"device-id",
Buffer (0x04)
{
    0xFF, 0x67, 0x00, 0x00
},
```

Model:

```dsl
"model",
Buffer ()
{
    "AMD Radeon RX 550"
}
```

`device-id` will be set to our PCI ID that we found in `Finding a suitable PCI ID` and `model` is mainly cosmetic

@another example:

so AMD Radeon RX 6950 XT final SSDT-GPU-SPOOF.dsl is: 

```dsl
// Based off of WhateverGreen's sample.dsl
// https://github.com/acidanthera/WhateverGreen/blob/master/Manual/Sample.dsl
DefinitionBlock ("", "SSDT", 2, "DRTNIA", "AMDGPU", 0x00001000)
{
    External (_SB_.PCI0, DeviceObj)
    External (_SB_.PCI0.GPP8.SWUS, DeviceObj)


    Scope (\_SB_.PCI0.GPP8.SWUS)
    {
        if (_OSI ("Darwin"))
        {
            Method (_DSM, 4, NotSerialized)  // _DSM: Device-Specific Method
            {
                Local0 = Package (0x04)
                {
                    // Where we shove our FakeID
                    "device-id",
                    Buffer (0x04)
                    {
                        0xBF, 0x73, 0x00, 0x00
                    },

                    // Changing the name of the GPU reported, mainly cosmetic
                    "model",
                    Buffer ()
                    {
                        "AMD Radeon RX 6950 XT"
                    }
                }
                DTGP (Arg0, Arg1, Arg2, Arg3, RefOf (Local0))
                Return (Local0)
            }
        }
    }
    Scope (\_SB.PCI0)
    {                   
        Method (DTGP, 5, NotSerialized)
        {
            If (LEqual (Arg0, ToUUID ("a0b5b7c6-1318-441c-b0c9-fe695eaf949b")))
            {
                If (LEqual (Arg1, One))
                {
                    If (LEqual (Arg2, Zero))
                    {
                        Store (Buffer (One)
                            {
                                 0x03
                            }, Arg4)
                        Return (One)
                    }

                    If (LEqual (Arg2, One))
                    {
                        Return (One)
                    }
                }
            }

            Store (Buffer (One)
                {
                     0x00
                }, Arg4)
            Return (Zero)
        }
      
    }

}
```

@another example:

so AMD Radeon RX 6650 XT final SSDT-GPU-SPOOF.dsl is: 

```dsl
// Based off of WhateverGreen's sample.dsl
// https://github.com/acidanthera/WhateverGreen/blob/master/Manual/Sample.dsl
DefinitionBlock ("", "SSDT", 2, "DRTNIA", "AMDGPU", 0x00001000)
{
    External (_SB_.PCI0, DeviceObj)
    External (_SB_.PCI0.GPP8.PBR0, DeviceObj)


    Scope (\_SB_.PCI0.GPP8.PBR0)
    {
        if (_OSI ("Darwin"))
        {
            Method (_DSM, 4, NotSerialized)  // _DSM: Device-Specific Method
            {
                Local0 = Package (0x04)
                {
                    // Where we shove our FakeID
                    "device-id",
                    Buffer (0x04)
                    {
                        0xFF, 0x73, 0x00, 0x00
                    },

                    // Changing the name of the GPU reported, mainly cosmetic
                    "model",
                    Buffer ()
                    {
                        "AMD Radeon RX 6650 XT"
                    }
                }
                DTGP (Arg0, Arg1, Arg2, Arg3, RefOf (Local0))
                Return (Local0)
            }
        }
    }
    Scope (\_SB.PCI0)
    {                   
        Method (DTGP, 5, NotSerialized)
        {
            If (LEqual (Arg0, ToUUID ("a0b5b7c6-1318-441c-b0c9-fe695eaf949b")))
            {
                If (LEqual (Arg1, One))
                {
                    If (LEqual (Arg2, Zero))
                    {
                        Store (Buffer (One)
                            {
                                 0x03
                            }, Arg4)
                        Return (One)
                    }

                    If (LEqual (Arg2, One))
                    {
                        Return (One)
                    }
                }
            }

            Store (Buffer (One)
                {
                     0x00
                }, Arg4)
            Return (Zero)
        }
      
    }

}
```

Now you're ready to compile the SSDT!

### [Compile ACPI final SSDT-GPU-SPOOF.dsl using Windows](https://dortania.github.io/Getting-Started-With-ACPI/Manual/compile.html#windows)

Compiling and decompiling on windows is fairly simple though, you will need [`iasl.exe`](https://acpica.org/downloads/binary-tools) and [`Command Prompt`](https://dortania.github.io/Getting-Started-With-ACPI/assets/img/windows-compile.62b90d74.png):

```
path/to/iasl.exe path/to/SSDT-GPU-SPOOF.dsl
```

## Cleanup

So you've made all your SSDTs but now there's one thing left: Adding them to OpenCore

The 2 main locations:

- EFI/OC/ACPI (Only .aml files, reminder to [compile your SSDTs](https://dortania.github.io/Getting-Started-With-ACPI/Manual/compile.html)
- config.plist -> ACPI -> Add

You can save yourself some work with the config.plist by running Cmd/Ctrl+R in ProperTree.
</details>

<details><summary>

## [🪄Creating your config.plist](https://dortania.github.io/OpenCore-Install-Guide/config.plist/#creating-your-config-plist)
</summary>
    
Now that we've got all our Kexts(.kext), SSDTs(.aml) and firmware drivers(.efi), your USB should start to look something like [this](https://dortania.github.io/OpenCore-Install-Guide/assets/img/populated-efi.8d46cc52.png)

> Note: Your USB will look different, everyone's system will have different requirements.

### Creating your config.plist

Enable File Extensions View in Windows File Explorer (Recommended): Open `File Explorer` (Windows + E). > Click the `View` tab on the top toolbar. > Hover over `Show` and select `File name extensions`.

First we'll want to grab the [Sample.plist](https://dortania.github.io/OpenCore-Install-Guide/assets/img/sample-location.9e091fb2.png) from the [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg/releases), this will be located under the `OpenCore\Docs` folder

Next lets move it onto our USB's EFI partition(will be called BOOT on Windows) under `EFI/OC/`, and rename it to [config.plist](https://dortania.github.io/OpenCore-Install-Guide/assets/img/renamed.9b06868d.png)

> Note: After copy Simple Properties file from `$env:USERPROFILE\Download\OpenCore\Docs\Sample.plist` path to `USB Drive\EFI\OC\Sample.plist`, right click on `Sample.plist` file then `Properties` then Rename this `Sample` to `config` also make sure `Type of file: Properties file Source File (.plist)`.

### Adding your SSDTs, Kexts and Firmware Drivers

For the rest of this guide, you're gonna need some form of plist editing. And for our guide, we'll be using ProperTree and GenSMBIOS to help automate some of the tedious work:

- [ProperTree](https://github.com/corpnewt/ProperTree)
 Universal plist editor

- [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
 For generating our SMBIOS data

Next, let's open ProperTree and edit our config.plist:

`ProperTree.bat`
 For Windows

`ProperTree.command`
 For macOS
> Pro tip: there's a buildapp.command utility in the Scripts folder that lets you turn ProperTree into a dedicated app in macOS

Once ProperTree is running, open your `config.plist` by pressing Cmd/Ctrl + O and selecting the config.plist file on your USB.

After the config is opened, press Cmd/Ctrl + Shift + R and point it at your EFI/OC folder to perform a `Clean Snapshot`:

This will remove all the entries from the `config.plist` and then adds all your SSDTs, Kexts and Firmware drivers to the config
Cmd/Ctrl + R is another option that will add all your files as well but will leave entries disabled if they were set like that before, useful for when you're troubleshooting but for us not needed right now

If you wish to clean up the file a bit, you can remove the `#WARNING` entries. Though they cause no issues staying there, so up to personal preference.

DANGER
 The `config.plist` must match the contents of the `EFI` folder. If you delete a file but leave it listed in the Config.plist, OpenCore will error and stop booting.

If you make any modifications, you can use the `OC snapshot` tool (Cmd/Ctrl + R) in ProperTree to update the `config.plist`.
</details>

<details><summary>

## 🛠️Alder / Raptor Lake Configs
</summary>

#### Alder Lake / Raptor Lake (12'th/13'th/14'th Gen intel Core)

Support|Version
:----|:----
Initial macOS Support|macOS 12, Monterey

### Starting Point

Now with all that, a quick reminder of the tools we need

- [ProperTree](https://github.com/corpnewt/ProperTree)

    Universal plist editor

- [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)

    For generating our SMBIOS data

- [Sample/config.plist](https://github.com/acidanthera/OpenCorePkg/releases)

    See previous section on how to obtain: [config.plist Setup](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#creating-your-configplist)

### ACPI

#### Add

> Info
> This is where you'll add SSDTs for your system, these are very important to booting macOS and have > many uses like USB maps
> (opens new window), disabling unsupported GPUs and such. And with our system, it's even required to > boot. Guide on making them found here: [Getting started with ACPI](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#alderlake--raptorlake-ssdts)

SSDT|Type|Enabled|Path|Comment
:----|:----|:----|:----|:----
★SSDT-HPET|Boolean|True|Root > ACPI > Add|to Fix Audio devices not being recognized.
★SSDT-EC|Boolean|True|Root > ACPI > Add|to manages critical functions, such as keyboard input, fan control, and charging.
☆SSDT-EC-USBX|Boolean|True|Root > ACPI > Add|Fix to your USB ports power management, fans controls by fixing Embedded Controller (EC).
★SSDT-PLUG-ALT|Boolean|True|Root > ACPI > Add|to manage Alder Lake and Raptor Lake CPU's power management.
★SSDT-RTCAWAC|Boolean|True|Root > ACPI > Add|to fix the system clocks.
SSDT-RHUB|Boolean|True|Root > ACPI > Add|only needed on Asus MB.
SSDT-Bridge|Boolean|True|Root > ACPI > Add|to Correct dGPU Unnamed PCI Bridges.
SSDT-DMAR|Boolean|True|Root > ACPI > Add|Intel I225 & Aquantia AQC113 Ethernet related.
SSDT-SBUS-MCHC|Boolean|True|Root > ACPI > Add|fixing many functions like: correct temperature, fan, voltage, etc readings (Proper Diagnostics).
SSDT-USBW|Boolean|True|Root > ACPI > Add|Fix a certain USB wakeup issue.
☆SSDT-DMAC|Boolean|True|Root > ACPI > Add|It helps avoid boot issues or ACPI errors related to missing DMAC.
SSDT-GPU-SPOOF|Boolean|True|Root > ACPI > Add|mainly needed for dGPUs that are not natively supported.
Spoof-SSDT|Boolean|True|Root > ACPI > Add|Disabling specific dGPU.
SSDT-DTPG|Boolean|True|Root > ACPI > Add|Thunderbolt related.
SSDT-UIAC|Boolean|True|Root > ACPI > Add|set port connector types (USB2/3).
> ★ mark are required

#### Delete
Deleting DMAR table might be necessary in certain cases, particularly on Intel systems with Thunderbolt or Ethernet support, to avoid conflicts with VT-d (Intel Virtualization Technology) for Directed I/O. This is important when using Thunderbolt, Ethernet or other peripherals that require AppleVTD to function correctly.

Delete|Type|Value|Path|Comment
:----|:----|:----|:----|:----
All|Boolean|True||
Comment|String|Delete standard DMAR table|Root > ACPI > Delete >|Thunderbolt, Intel I225 & Aquantia AQC113 Ethernet related
Enabled|Boolean|True||
OemTableId|Data|||
TableLength|Number|0||
TableSignature|Data|444D4152||

#### Patch

This section allows us to dynamically modify parts of the ACPI (DSDT, SSDT, etc.) via OpenCore. For us, our patches are handled by our SSDTs. This is a much cleaner solution as this will allow us to boot Windows and other OSes with OpenCore

Fix wake from sleep issue on Gigabyte/Asus Z690 boards (Optional):

Fix ACPI error on Gigabyte Z690 boards:

Patch|Type|Value|Path
:----|:----|:----|:----
Comment|String|Change ADBG to XDBG|Root > ACPI > Patch
Count|Number|1|
Enabled|Boolean|True|
Find|Data|4303141941444247|
OemTableId|Data|475357417070|
Replace|Data|4303141958444247|
TableLength|Number|0|
TableSignature|Data|53534454|

Fix ACPI error on Asus Z690 boards:

Patch|Type|Value|Path
:----|:----|:----|:----
Comment|String|Change MC__ to MCHC|Root > ACPI > Patch
Count|Number|0|
Enabled|Boolean|True|
Find|Data|4D435F5F|
OemTableId|Data|4967667853736474|
Replace|Data|4D434843|
TableLength|Number|0|
TableSignature|Data|53534454|

#### Quirks

Settings relating to ACPI, leave everything here as default as we have no use for these quirks.

### Booter

#### MmioWhitelist
This section is allowing devices to be passthrough to macOS that are generally ignored, for us we can ignore this section.

#### Quirks

Settings relating to boot.efi patching and firmware fixes, for us, we need to change the following

Quirks|Type|Value|Path|Comment
:----|:----|:----|:----|:----
DevirtualiseMmio|Boolean|False|Root > Booter > Quirks|
EnableWriteUnprotector|Boolean|False|Root > Booter > Quirks|
ProtectUefiServices|Boolean|True|Root > Booter > Quirks|
RebuildAppleMemoryMap|Boolean|True|Root > Booter > Quirks|
ResizeAppleGpuBars|Numbers|-1|Root > Booter > Quirks|if your set ResizeAppleGpuBars=-1 also set `Re-Size BAR Support` = `Disabled` in BIOS. if you are using RX 6600 or newer series GPU means your dGPU support ResizeBars so set ResizeAppleGpuBars=0 and also set `Re-Size BAR Support` = `Enabled` in your Motherboard BIOS.
SetupVirtualMap|Boolean|True|Root > Booter > Quirks|This quirk is required for the majority of firmwares and without it it's very common to kernel panic here, so enable it if not already. However, certain firmwares(mainly 2020+) do not work with this quirk and so may actually cause this kernel panic.
SyncRuntimePermissions|Boolean|True|Root > Booter > Quirks|

#### DeviceProperties

##### Add

###### AMD GPU Secific DeviceProperties

AMD GPU|DeviceProperties Path|Type|Value|Path
:----|:----|:----|:----|:----
|                       |   DeviceProperties                                                 |          |                 |
|                       |                  └──Add                                            |          |                 |
AMD Radeon RX 550 (Lexa)|                        └── PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)  |Dictionary|                 |Root > DeviceProperties > Add
|                       |                            ├── device-id                           |Data      |FF670000         |
|                       |                            ├── model                               |String    |AMD Radeon RX 550|
|                       |                            └── no-gfx-spoof                        |Data      |01000000         |

[PCI / Device ID Repo](https://pci-ids.ucw.cz/read/PC/1002)

> [!NOTE]
> `no-gfx-spoof` flag use to fix conflicts or graphical glitches with spoofing enabled, gpu doesn't get detected properly with the spoof, certain application not detect your gpu.

Others common flag can be use in this card (WARNING: Try your own risk):

- `-no_compat_check`: Avoids compatibility checks (sometimes helpful if you run into issues with unsupported hardware).

- `-disablegfxfirmware`: This might be needed for Polaris GPUs (like the AMD Radeon RX 550) to prevent a macOS firmware check that can cause issues.

- `-radpg`: This can help with enabling AMD GPU acceleration.

GPU `model`|`device-id`
:----|:----
AMD Radeon RX 550|FF67
AMD Radeon RX 560|FF670000
AMD Radeon RX 6950 XT|BF730000
AMD RX 6900XTHT|BF730000
AMD Radeon RX 6600|FF730000
AMD Radeon RX 6600 XT|FF730000
AMD Radeon RX 6650 XT|FF730000

> [!NOTE]
> if `device-id` not work add `0000` last of `device-id` (ie. `FF670000`)

*by format of a fake ID:

```dsl
"device-id",
Buffer (0x04)
{
     0xFF, 0x67, 0x00, 0x00
},
```

@another example:
AMD GPU|DeviceProperties Path|Type|Value|Path
:----|:----|:----|:----|:----
|                      |   DeviceProperties                                                                           |          |                             |
|                      |                  └──Add                                                                      |          |                             |
Radeon RX 6950 XT      |                        └── PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)  |Dictionary|                             |Root > DeviceProperties > Add
|                      |                            ├── device-id                                                     |Data      |BF730000                     |
|                      |                            └── model                                                         |String    |Radeon RX 6950 XT 16 GB GDDR6|

@another example:
AMD GPU|DeviceProperties Path|Type|Value|Path
:----|:----|:----|:----|:----
|                      |   DeviceProperties                                                                           |          |                             |
|                      |                  └──Add                                                                      |          |                             |
Radeon RX 6650 XT      |                        └── PciRoot(0x0)/Pci(0x3,0x1)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)  |Dictionary|                             |Root > DeviceProperties > Add
|                      |                            ├── device-id                                                     |Data      |FF730000                     |
|                      |                            └── model                                                         |String    |Radeon RX 6650 XT 8 GB GDDR6 |

Disabling specific dGPU using DeviceProperties:

Here is quite simple, find the PCI route with Windows `Device Manager` and then create a new DeviceProperties section with your spoof:

And the PCI Path will Final in something similar:

`PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)`

With this, navigate towards `Root -> DeviceProperties -> Add` and add your final PCI Path with the following properties:

Key|Type|Value|Path|Comment
:----|:----|:----|:----|:----
disable-gpu|Boolean|True|Root -> DeviceProperties -> Add -> dGPU final PCI Path that you want to disable|this will Disables GPU on a per-slot basis

###### Intel's I225-V 2.5GbE controller Secific DeviceProperties

PciRoot(0x0)/Pci(0x1C,0x1)/Pci(0x0,0x0)

This entry relates to Intel's I225-V 2.5GbE controller found on higher end Alder/Raptor Lake boards, what we'll be doing here is tricking Apple's I225LM driver into supporting our I225-V network controller:

Key|Type|Value|Path
:----|:----|:----|:----
device-id|Data|F2150000|Root > DeviceProperties > Add > PciRoot(0x0)/Pci(0x1C,0x1)/Pci(0x0,0x0)

> Note: If your board didn't ship with the Intel I225 NIC, there's no reason to add this entry.
> Note 2: If you get a kernel panic on the AppleIntelI210Ethernet.kext, your Ethernet's path is likely PciRoot(0x0)/Pci(0x1C,0x4)/Pci(0x0,0x0)

###### Fix AQC113 (Optional)

Key|Type|Value|Path
:----|:----|:----|:----
AAPL,slot-name|String|Internal@0,1,0/0,0|Root > DeviceProperties > Add > PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)
compatible|Data|70636931 6436612C 39346330 000000|
device-id|Data|C0940000|
device_type|String|Ethernet controller|
model|String|Aquantia AQC113|

###### AppleALC audio injection:

[AppleALC Supported Codecs](https://github.com/acidanthera/AppleALC/wiki/Supported-codecs)
find your Audio controller PCI Path and Codec. for my case Audio Controller ALC897 PCI Path is `PciRoot(0x0)/Pci(0x1F,0x3)` and Codec is `11`
so, replace `PciRoot(0x0)/Pci(0x1b,0x0)` with your Audio Controller Path and `layout-id` type as `Number` with your Audio Codec value. for my case:
Key|Type|Value|Path
:----|:----|:----|:----
layout-id|Number|11|Root > DeviceProperties > Add > ~~PciRoot(0x0)/Pci(0x1b,0x0)~~ → PciRoot(0x0)/Pci(0x1f,0x3)

Baffin HDMI/DP Audio [Radeon RX 550 640SP / RX 560/560X] PCI Path: PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x1)

###### [Fixing en0](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-en0)

- find the PciRoot of your ethernet controller using `Device Manager` > `Propaties` > `Location Path`. for my case Realtek RTL8125 2.5GbE Ethernet Controller, this would be `PciRoot(0x0)/Pci(0x1c,0x2)/Pci(0x0,0x0)`

- Now with the PciRoot, go into your `config.plist` -> `DeviceProperties` -> `Add`

Key|Type|Value|Path
:----|:----|:----|:----
built-in|Data|01|Root > DeviceProperties > Add > PciRoot(0x0)/Pci(0x1c,0x2)/Pci(0x0,0x0)

[ie.](https://dortania.github.io/OpenCore-Post-Install/assets/img/config-built-in.511f620e.png)

##### Delete

Removes device properties from the map, for us we can ignore this

#### Kernel

##### Add

Here's where we specify which kexts to load, in what specific order to load, and what architectures each kext is meant for. By default we recommend leaving what ProperTree has done

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Before macOS installation (if you need internet during macOS installation):

Key|Type|Value|Path|Note
:----|:----|:----|:----|:----
BundlePath|String|itlwm.kext|Root > Kernel > Add >|
Enabled|Boolean|False||set as `False` if you have exist both `itlwm.kext` & `AirportItlwm.kext` in your OpenCore `EFI > OC > Kexts` folder.

Key|Type|Value|Path|Note
:----|:----|:----|:----|:----
BundlePath|String|AirportItlwm.kext|Root > Kernel > Add >|
Enabled|Boolean|True||set as `True` if you need internet during macOS installation.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

After macOS installation (if you need iMessages Services after macOS installation):

Key|Type|Value|Path|Note
:----|:----|:----|:----|:----
BundlePath|String|itlwm.kext|Root > Kernel > Add >|
Enabled|Boolean|True||set as `True` if you need iMessages Services after macOS installation. Required [Heliport.dmg](https://github.com/OpenIntelWireless/HeliPort/releases) client for connecting WiFi.

Key|Type|Value|Path|Note
:----|:----|:----|:----|:----
BundlePath|String|AirportItlwm.kext|Root > Kernel > Add >|
Enabled|Boolean|False||set as `False` if you have exist both `itlwm.kext` & `AirportItlwm.kext` in your OpenCore `EFI > OC > Kexts` folder.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##### Block

Blocks certain kexts from loading. Not relevant for us.

##### Emulate

Needed for spoofing unsupported CPUs, thankfully in 12+ Alder/Raptor Lake S support was CPU ID is set to 0x0A0655 that is found in Comet Lake CPUs such as [10900, 10850, 10700, and 10400](https://www.cpu-world.com/cgi-bin/CPUID.pl?MANUF=Intel&FAMILY=&MODEL=&SIGNATURE=656981&PART=&ACTION=Filter) so need to spoof `0x0A0655` here.
 This is required for Alder Lake. The configurations universally use these settings:

As Alder/Raptor Lake CPUs are not supported by macOS, the CPU ID has to be faked in the Config.plist

Emulate|Type|Value|Path
:----|:----|:----|:----
Cpuid1Data|Data  |  55060A00 00000000 00000000 00000000 |
Cpuid1Mask|Data  |  FFFFFFFF 00000000 00000000 00000000 |Root > Kernel > Emulate
MinKernel |String|   19.0.0                             |

##### Force

 Used for loading kexts off system volume, only relevant for older operating systems where certain kexts are not present in the cache(ie. IONetworkingFamily in 10.6).

 For us, we can ignore.

##### Patch

 Patches both the kernel and kexts.

 ##### Quirks

> Info
> Settings relating to the kernel, for us we'll be enabling the following:

Quirk|Type|Value|Comment|Path
:----|:----|:----|:----|:----
AppleXcpmCfgLock|Boolean|False|Disabling CFG-Lock in the BIOS allows macOS (and the bootloader) to modify the CPU registers freely, ensuring smooth CPU power management without additional patches. Setting AppleXcpmCfgLock to True is only necessary when the BIOS has CFG-Lock enabled and you cannot disable it.|
AppleXcpmForceBoost|Boolean|False||Root > Kernel > Quirks
DisableIoMapper|Boolean|False|if you set DisableIoMapper=False, Please Disabled `VT-D` in BIOS. Thunderbolt, Intel I225 & Aquantia Ethernet related|
ForceAquantiaEthernet|Boolean|False|set ForceAquantiaEthernet=True if your Motherboard has Aquantia (AQC113) based Ethernet Controller|
PanicNoKextDump|Boolean|True||Root > Kernel > Quirks
PowerTimeoutKernelPanic|Boolean|True||
ProvideCurrentCpuInfo|Boolean|True|More patches are required for XNU when using the efficiency cores, though handled automatically by the ProvideCurrentCpuInfo quirk starting with OpenCore|
XhciPortLimit|Boolean|False|macOS Moterey 12+ no need this|

##### Scheme

 Settings related to legacy booting(ie. 10.4-10.6), for majority you can skip

### Misc

#### Boot

Quirk|Type|Value|Comment|Path
:----|:----|:----|:----|:----
HideAuxiliary|Boolean|False|don't need to press `Space` key on your keyboard to show macOS recovery and other auxiliary entries|Root > Misc > Boot
PickerAttributes|Number|17|This enables mouse/trackpad support as well as [.VolumeIcon.icns](https://github.com/acidanthera/OcBinaryData/tree/master/Resources/Image/Acidanthera/GoldenGate) reading from the drive, allows for macOS installer icons to appear in the picker|
PickerMode|String|External|`Builtin` - by Default|
PickerVariant|String|Acidanthera\GoldenGate|`Auto` — Automatically select one set of icons based on DefaultBackground colour. [Acidanthera\Syrah](https://dortania.github.io/OpenCore-Post-Install/assets/img/gui.a10019ae.png) — Normal icon set. [Acidanthera\GoldenGate](https://dortania.github.io/OpenCore-Post-Install/assets/img/gui-nouveau.8ad4a7b4.png) — Nouveau icon set. [Acidanthera\Chardonnay](https://dortania.github.io/OpenCore-Post-Install/assets/img/gui-old.53c75c16.png) — Vintage icon set. [..more](https://dortania.github.io/OpenCore-Post-Install/cosmetic/gui.html#setting-up-opencore-s-gui)

#### Debug

Debug|Type|Value|Path|Comment
:----|:----|:----|:----|:----
AppleDebug|Boolean|True|Root > Misc > Debug|
ApplePanic|Boolean|True|Root > Misc > Debug|
DisableWatchDog|Boolean|True|Root > Misc > Debug|
Target|Number|67|Root > Misc > Debug|3=enableOnscreenDebug(recommended after macOS installation/updating); 67=enableOnscreenDebug+enableLogging2File(recommended during macOS installation/updating)

#### Entries

Used for specifying irregular boot paths that can't be found naturally with OpenCore.

#### Security

> Info
> Security is pretty self-explanatory, do not skip. We'll be changing the following:

Quirk|Type|Value|Path|Comment
:----|:----|:----|:----|:----
AllowSetDefault|Boolean|True||
BlacklistAppleUpdate|Boolean|False||False will allow macOS update using macOS System Preferences > Software Update.
EnablePassword|Boolean|False||this will Enable [OpenCore Menu Password](https://dortania.github.io/OpenCore-Post-Install/universal/security/password.html)
ExposeSensitiveData|Number|6||Shows more debug information, requires debug version of OpenCore.
PasswordHash|Data|||Related to `EnablePassword`. Hash of the OpenCore Menu Password.
PasswordSalt|Data|||Related to `EnablePassword`. Ensures 2 users with the exact same password do not have the same hash.
ScanPolicy|Number|0|Root > Misc > Security|this quirk allows to prevent scanning and booting from untrusted sources. Setting to `0` will allow all sources present to be bootable
SecureBootModel|String|Disabled||as `Default` for OpenCore to automatically set the correct value corresponding to your SMBIOS. This enables security features such as the verification of macOS' `boot.efi`, with restricting which macOS versions OpenCore will boot. `Default` set to `x86legacy` Recommended for VMs.
Vault|String|Optional||[more info](https://dortania.github.io/OpenCore-Post-Install/universal/security/vault.html)
#### Serial

 Used for serial debugging (Leave everything as default).

#### Tools

 Used for running OC debugging tools like the shell, ProperTree's snapshot function will add these for you.

### NVRAM

#### Add

NVRAM|child|Type|Value|Comment|Path
:----|:----|:----|:----|:----|:----
4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102|revcpuname|String|3.3 GHz Quad-Core Intel Core i3|add your CPU name here. in Recommended Format: `Intel® Core™ i3-12100F` / `Intel Core i3-12100F` / `3.3 GHz Intel Core i3` / `3.3 GHz Quad-Core Intel Core i3` / `3.3 GHz 4-Core Intel Core i3` / `4-Core Intel i3-12100F`|Root > NVRAM > Add
||revcpu|Number|1||
7C436110-AB2A-4BBB-A880-FE41995C9F82|SystemAudioVolume|Data|46|This is the boot-chime and screen reader volume, note it's in hexadecimal so would become `70` in decimal; `80` is mute|
||boot-args|String|-v keepsyms=1 debug=0x100 unfairgva=1 -radcodec alcid=11 revpatch=sbvmm|`-v` this flag enable verbose mode, it's can help you identify issues, problem kexts, etc during boot; `debug=0x100` this disables macOS's watchdog which helps prevents a reboot on a kernel panic. That way you can hopefully glean some useful info and follow the breadcrumbs to get past the issues; `keepsyms=1` this flag is a companion setting to debug=0x100 that tells the OS to also print the symbols on a kernel panic. That can give some more helpful insight as to what's causing the panic itself; `unfairgva=1` Used for fixing hardware DRM support on supported AMD GPUs; `-radcodec` used for allowing officially unsupported AMD GPUs (spoofed) to use the Hardware Video Encoder; `alcid=X` Used for setting layout-id for AppleALC, see [supported codecs](https://github.com/acidanthera/applealc/wiki/supported-codecs). X=YourMotherbordOnboardAudioCodecLayout (for Realtek ALC897 Audio Codec Layout = 11); `revpatch=sbvmm` used for pertains with RestrictEvents.kext to modifying system behavior during the boot process; `-lilubetaall` used for enable macOS beta or debug features in the Lilu.kext (its provide patch WhateverGreen.kext: AMD GPU kext, AppleALC: Audio kext, VirtualSMC: its provide power management, fan control, thermal readings etc.)|Root > NVRAM > Add
||prev-lang:kbd|String|en-US:0|or `prev-lang:kbd` `Data` `656e2d55533a30` Hexadecimal is a way to represent Numbers, It uses 16 symbols (0-9 and A-F).`en-US:0` refers to the standard `US English` keyboard layout. This is the most common layout, The value of `prev-lang:kbd` appears as a hexadecimal, this ensures that your keyboard input is recognized correctly during the macOS installation process. In [AppleKeyboardLayouts.txt](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt), you'll find the string `en-US:0`, Convert `en-US:0` string to hex, which gives you `656e2d55533a30` (Using a [string-to-hex converter](https://codebeautify.org/string-hex-converter)).|
||StartupMute|Data|00|Optional: Mute startup chime sound in firmware audio support; 0x00 is unmuted, missing variable or any other value means muted.|

> info
> if you are using `intel-Core-ix-1xxxxx` processor that comes with `Intel-UHD-Graphics-730` this iGPU not supported in OpenCore to disable this unsupported igpu please used this flag `-wegnoigpu`.
> if you are using `intel-Core-ix-1xxxxxF` processor means no iGPU, remove `-wegnoigpu` flag.

> using [CpuTopologyRebuild.kext](https://github.com/b00t0x/CpuTopologyRebuild/releases) with the `-ctrsmt` boot arg, which makes MacOS see the E-Cores as additional SMT threads, if your CPU has `E-Cores`.

> if you are using Radoen RX 5000 & 6000 series `Navi` GPUs (ie. AMD Radeon RX 6600) to disabling board ID checks used `agdpmod=pikera` flag, without this you'll get a black screen. if you are using `Polaris` (ie. AMD Radeon RX 550) and `Vega` cards don't use this.
for more info see [AMD GPU Support](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html#native-amd-gpus)

GPU|Boot argument
:----|:----
AMD Radeon RX 550|-radcodec
AMD Radeon RX 560|-radcodec
AMD Radeon RX 570|-radcodec
AMD Radeon RX 6800|agdpmod=pikera
AMD Radeon RX 6800 XT|agdpmod=pikera
AMD Radeon RX 6900 XT|agdpmod=pikera
AMD Radeon RX 6950 XT|agdpmod=pikera
AMD Radeon RX 6600|agdpmod=pikera
AMD Radeon RX 6600 XT|agdpmod=pikera
AMD Radeon RX 6650 XT|agdpmod=pikera

##### Some other popular Audio Codec layout:

Audio Codec|Layout|Common Layout
:----|:----|:----
Realtek ALC897|11, 12, 13, 21, 23, 66, 69, 77, 98, 99|11
Realtek ALC1220|1, 2, 3, 5, 7, 11, 13, 15, 16, 17, 18, 20, 21, 25, 27, 28, 29, 30, 34, 35, 98, 99, 100|11
Realtek ALCS1220A|1, 2, 3, 5, 7, 8, 11, 13, 15, 20, 21, 99|11
Realtek ALC887|1, 2, 3, 5, 7, 11, 12, 13, 17, 18, 20, 33, 40, 50, 52, 53, 87, 99|11
Realtek ALC1200|1, 2, 3, 4, 5, 7, 11, 27, 28, 29|11
~~Realtek ALC4080~~|-|
~~Realtek ALC4082~~|-|
~~Realtek ALC4050~~|-|

#### Delete

##### LegacySchema
Used for assigning NVRAM variables, used with `OpenVariableRuntimeDxe.efi`. Only needed for systems without native NVRAM

> Info: Forcibly rewrites NVRAM variables, do note that Add will not overwrite values already present in NVRAM so values like boot-args should be left alone. For us, we'll be changing the following:

Delete|Type|Value|Path
:----|:----|:----|:----
LegacyOverwrite|Boolean|False|Root > NVRAM > Delete
WriteFlash|Boolean|True|Root > NVRAM > Delete

### PlatformInfo

### [Fixing ROM](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-rom)

Derive the corresponding ROM Value

> NOTE
> For ROM, we use the MAC Address of the network interface, lowercase, and without `:`

`ROM` is calculated from your `MAC Address`.

- Windows: Settings -> Network & Internet -> Ethernet -> Ethernet -> Physical MAC Address

Lowercase your `MAC Address`, and remove each colon `:` between the octets.

For example:

MAC: `00:16:CB:00:11:22`

ROM: `0016cb001122`

add your `ROM` value to `config.plist` -> `PlatformInfo` -> `Generic` -> ROM = 0016cb001122

ROM|Type|Value|Path
:----|:----|:----|:----
ROM|Data|0016cb001122|Root > PlatformInfo > Generic

[ie.](https://dortania.github.io/OpenCore-Post-Install/assets/img/config-rom.faa79c0f.png)

> Info
> For setting up the SMBIOS info, we'll use CorpNewt's [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) application.

macOS|SystemProductName|Recommended before macOS update/ installaion|Recommended after macOS update/ installaion|Comments
:----|:----|:----|:----|:----
12 Monterey|`MacPro7,1`, `iMac20,1`, `iMacPro1,1`, `iMac19,1`|`MacPro7,1`|`iMac20,1`|macOS Monterey & Ventura recommended SMBIOS are same
14 Sonoma|`MacPro7,1`, `iMac20,1`, `iMacPro1,1`, `iMac19,1`|`iMac19,1` with `revpatch=sbvmm` boot-args|`iMac19,1`|if you using `iMac19,1` please add `revpatch=sbvmm` boot-args in config.plist Root > NVRAM > Add > 7C436110-AB2A-4BBB-A880-FE41995C9F82
15 Sequoia|`MacPro7,1`, `iMac20,1`, `iMacPro1,1`, `iMac19,1`|`iMac19,1` with `revpatch=sbvmm` boot-args|`iMac19,1`|
26 Tahoe|`MacPro7,1`, `iMac20,1`|`MacPro7,1`|`iMac20,1`|`AppleALC.kext` is broken, `WhateverGreen.kext` is bugged on AMD 6000 series cards, please disabled `IntelBTPatcher.kext`, `IntelMausi.kext` may not work.

[Mac Pro (2019)](https://support.apple.com/en-in/118461) = `MacPro7,1` max macOS Sequoia

[iMac (Retina 5K, 27-inch, 2020)](https://support.apple.com/en-in/111913) = `iMac20,1` max macOS Tahoe

[iMac Pro (2017)](https://support.apple.com/en-in/111995) = `iMacPro1,1` max macOS Sequoia

[iMac (Retina 5K, 27-inch, 2019)](https://support.apple.com/en-in/111998) = `iMac19,1` max macOS Sequoia

download and extract GenSMBIOS.zip then go to extracted GenSMBIOS folder then double click on `GenSMBIOS.bat` file chose `Install/Update MacSerial` by enter `1` then `Select config.plist` option by pick `2` then drag-and-drop your OpenCore config.plist from USB Drive then press `Enter` then chose `Generate SMBIOS` option by enter `3` then enter `iMac19,1` then `Q`.

> For this Alder/Raptor Lake example, we'll chose the `iMac19,1` SMBIOS - this is done intentionally for compatibility's sake. There are two main SMBIOS used for Alder/Raptor Lake: `iMac19,1` and `MacPro7,1`. Read this for details: [Choosing the right SMBIOS | OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/extras/smbios-support.html#choosing-the-right-smbios).

### UEFI

#### APFS

By default, OpenCore only loads APFS drivers from macOS 12+

APFS|Type|Value|Path|Comment
:----|:----|:----|:----|:----
EnableJumpstart|Boolean|False|Root > UEFI > APFS|Fix: macOS Tahoe turns FileVault on automatically.

#### Audio

Related to AudioDxe settings, for us we'll be changing(editing as hardware specific). This is unrelated to audio support in macOS. [..more](https://dortania.github.io/OpenCore-Post-Install/cosmetic/gui.html#setting-up-boot-chime-with-audiodxe)

Audio|Type|Value|Path|Comment
:----|:----|:----|:----|:----
AudioCodec|Number|0|Root > UEFI > Audio|AudioCodec in AudioDxe (OpenCore Audio Driver), `0` acts as a default setting. In some cases, it might correspond to a Layout-Specific Codecs depends on the your Codec address of Audio controller. This typically contains the first audio codec address on the builtin analog audio controller (HDEF).
AudioDevice|String|PciRoot(0x0)/Pci(0x1f,0x3)||It defines the PCI Path of your onboard audio controller.
AudioOutMask|Number|-1||Play sound in UEFI to more than one channel, value is `-1` = output to all speaker.
AudioSupport|Boolean|True||this will activates AudioDxe.efi. Enabling this setting routes audio playback from builtin protocols to specified dedicated audio ports (AudioOutMask) of the specified codec (AudioCodec), located on the specified audio controller (AudioDevice)
MaximumGain|Number|-15||Maximum gain to use for UEFI audio, specified in decibels (dB) with respect to amplifier reference level of 0 dB
MinimumAssistGain|Number|-30||Minimum gain in decibels (dB) to use for picker audio assist. The screen reader will use this amplifier gain if the system amplifier gain read from the SystemAudioVolumeDB NVRAM variable is lower than this
MinimumAudibleGain|Number|-55||Minimum gain in decibels (dB) at which to attempt to play any sound
PlayChime|String|Enabled||This enables the iconic macOS boot chime. [OCEFIAudio_VoiceOver_Boot.mp3](https://github.com/acidanthera/OcBinaryData/blob/master/Resources/Audio/OCEFIAudio_VoiceOver_Boot.mp3) file required for the Boot-Chime. make sure this file exist on `EFI/OC/Audio/OCEFIAudio_VoiceOver_Boot.mp3`.`Auto` — Enables chime when StartupMute NVRAM variable is not present or set to 00. `Enabled` — Enables chime unconditionally. `Disabled` — Disables chime unconditionally.
ResetTrafficClass|Boolean|False||This can sometimes resolve issues with audio initialization.
SetupDelay|Number|0||This introduces a delay (in milliseconds) before the boot chime plays. It gives the audio hardware extra time to initialize. Some codecs many need extra time for initialize, we recommend setting to 500 milliseconds (0.5 seconds) if you have issues.

> Note: `AudioDevice` Value depand on Onboard Audio Controller(Codec) for my case Realtek ALC897 so my audio controller PCI Path: PciRoot(0x0)/Pci(0x1f,0x3)

#### Drivers

Add your .efi drivers here.

Only drivers present here should be:

    - HfsPlus.efi
    - OpenRuntime.efi

#### Input

Related to boot.efi keyboard passthrough used for FileVault and Hotkey support, leave everything here as default as we have no use for these quirks.

#### Output

 Relating to OpenCore's visual output.

Output|Type|Value|Path|Comment
:----|:----|:----|:----|:----
ProvideConsoleGop|Boolean|True|Root > UEFI > Output|its fixes black screen

#### ProtocolOverrides
Mainly relevant for Virtual machines, legacy macs and FileVault users.

#### Quirks

> Info: Relating to quirks with the UEFI environment, for us we'll be leave everything here as default.

#### ReservedMemory
Used for exempting certain memory regions from OSes to use, mainly relevant for Sandy Bridge (2nd-Gen Intel Core ix) iGPUs or systems with faulty memory. Use of this quirk is not covered in this guide

### Cleaning up

And now you're ready to save and place it into your EFI under EFI/OC.

### Generating our SMBIOS data:

Download [GenSMBIOS.zip](https://github.com/corpnewt/GenSMBIOS)

- Extract `GenSMBIOS.zip` > Open `GenSMBIOS` Folder > Double click `GenSMBIOS.bat` > `More info` > `Run Anyway`

- chose `Install/Upadate MacSerial` by pick `1` > hit `Enter` key

- chose `Select config.plist` by pick `2` > hit `Enter` > drag and drop `config.plist` form our `USB Drive` `USB Drive:\\EFI\OC\config.plist` > hit `Enter`

- chose `Generate SMBIOS` by pick `3` > hit `Enter` > type `iMac19,1` > hit `Enter` > hit `Enter`

- chose `Generate UUID` by pick `4` > hit `Enter` > hit `Enter`

- pick `Q` to quit from `GenSMBIOS.bat`

### Update Motherboard BIOS:

#### Check Motherboard BIOS version in Windows:

- Press `Windows key` + `R` on your keyboard then press `Ok` or `Enter`
- Type from `cmd`:
  ```
  wmic bios get smbiosbiosversion
  ```
  then press `Enter`.
- Now you see following `SMBIOSBIOSVersion` : `F33`

#### Check Motherboard BIOS Update:

- Search your motherboard model in [Google](https://www.google.com/) for [my case](https://www.google.com/search?q=gigabyte+b660m+ds3h+ax+ddr4) i'm using `Gigabyte B660M DS3H AX DDR4`
- then click on first link for [my case](https://www.gigabyte.com/Motherboard/B660M-DS3H-AX-DDR4-rev-1x)
- then `Support` for [my case](https://www.gigabyte.com/Motherboard/B660M-DS3H-AX-DDR4-rev-1x/support)
- then `Downloads`
- then `BIOS` for [my case](https://www.gigabyte.com/Motherboard/B660M-DS3H-AX-DDR4-rev-1x/support#Support-Bios)
- Now you see your motherboard latest BIOS version (for my case: `F34`)
- Now compare both `motherbord latest` and `SMBIOSBIOSVersion`
- after compare if you found any diffrent (for my case: `F34 vs F33`), follow BIOS Update Guide

#### Update BIOS:

> [!WARNING]
> before update motherboard BIOS, make sure your computer have stable internet connection during BIOS download & your computer powerup by Uninterruptible Power Source, if not your motherboard BIOS chip will corrupted during update & your motherboard dead permanently.

##### `Gigabyte B660M DS3H AX DDR4` BIOS Update:
- format your USB Drive as FAT32:
  - using Windows `Disk Management`:
    - Open `Disk Management` > Removable Disk > right click `Format...` > Volume label: `USB Drive`; File system: `FAT32` then click `OK` then `OK`.
  - using rufus:
    - Download [rufus-x.exe](https://github.com/pbatard/rufus/releases)
    - double click `rufus-x.exe` then `Yes` then `Yes`
    - from `Rufus` - Device: `USB Drive`; Boot selection: `Non bootable`; Partition scheme: `MBR`; Volume label: `USB Drive`; File system: `Large FAT32 (Default)` then click `START` then `OK`.
- delete USB Drive multiple partitions:
  - Open `Disk Management` > Removable Disk > right click any partitions of Removable Disk > Delete Volume... > Yes.
- Download latest BIOS.zip from your motherboard official website. (for [my case](https://www.gigabyte.com/Motherboard/B660M-DS3H-AX-DDR4-rev-1x/support#Support-Bios))
  - right click `mb_bios_b660m-ds3h-ax-ddr4_f34.zip`
  - then chose `Extract All...` then `Extract`
  - copy `mb_bios_b660m-ds3h-ax-ddr4_f34` folder to your `USB Drive` root directory
- Flash BIOS:
  - insert `USB Drive` on your computer USB port
  - `Restart` your computer and press `Delete` key on your keyboard

     or right click `Windows Start` icon > `Shutdown or sign out` > hold `Shift` key & `Restart` > `Troublesshoot` > `Advaced options` > `UEFI Firmware Settings` > `Restart` or press `Enter` key.
  - from motherboard BIOS menu: chose `Q-Flash` then `Update BIOS` then go to your `USB Drive` root directory then `mb_bios_b660m-ds3h-ax-ddr4_f34` folder then chose `B660MDS3HAXDDR4.F34` file and press flash button then Are you sure to update BIOS?: `Yes`.
  - Now you see BIOS Update progress bar
  - wait few minutes until BIOS update, your computer restart one or several times.
  - Check Motherboard BIOS version in Windows

### [Intel BIOS settings](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#intel-bios-settings)

- `Restart` your computer > press `Delete` key on your keyboard

   or right click `Windows Start` icon > `Shutdown or sign out` > hold `Shift` key & `Restart` > `Troublesshoot` > `Advaced options` > `UEFI Firmware Settings` > `Restart` or press `Enter` key.

#### Gigabyte B660M DS3H DDR4 (BIOS_F34) BIOS Settings

Settings|Value|Path|Comment
:----|:----|:----|:----
Above 4G Decoding|Enabled|ADVANCED MODE > Settings > IO Ports > Above 4G Decoding = Enabled|
Re-Size BAR Support|Disabled|ADVANCED MODE > Settings > IO Ports > Re-Size BAR Support = Disabled|please Enabled it if you are using AMD Radeon RX 6600 or newer card, this is potentially boost your system's performance if your GPU Support it. if you set `Re-Size BAR Support` = `Enabled` in your Motherboard BIOS, make sure you set ResizeAppleGpuBars=0 value on config.plist Root > Booter > Quirks
Super IO Congratulation|Disabled|ADVANCED MODE > Settings > IO Ports > Super IO Congratulation > Serial Port = Disabled|
XHCI Hand-off|Enabled|ADVANCED MODE > Settings > IO Ports > USB Configuration> XHCI Hand-off = Enabled|
SATA Controller|Default/AHCI|ADVANCED MODE > Settings > IO Ports > > SATA Configuration > SATA Mode or  SATA Controller : AHCI|if you have SATA drive change SATA Mode to `AHCI` otherwise leve it `Default`
Intel PTT|Enabled|ADVANCED MODE > Settings >  Miscellaneous > Intel PTT = Enabled|Warning!: Windows required `Intel PTT`, if you disable this you can't boot Windows alongside macOS anymore...
VT-d|Disabled|ADVANCED MODE > Settings >  Miscellaneous > VT-d = Disabled|
Hyper-Threading Technology|Enabled|ADVANCED MODE > Tweaker > Advanced CPU Settings > Hyper-Threading Technology = Enabled|
VT-x|Enabled|ADVANCED MODE > Tweaker > Advanced CPU Settings > Intel (VMX) Virtualization Technology or VT-x = Enabled|
Extreme Memory Profile(X.M.P.)|Profile1|ADVANCED MODE > Tweaker > Extreme Memory Profile(X.M.P.) = Profile1|A Intel technology that allows users to overclock their memory to enhance performance
CFG Lock|Disabled|ADVANCED MODE > Boot > CFG Lock = Disabled|from USB Drive config.plist Root > Kernel > Quirks > AppleXcpmCfgLock = False
Fast Boot|Disabled|ADVANCED MODE > Boot > Fast Boot = Disabled|
Windows 10 Features|Other OS|ADVANCED MODE > Boot > Windows 10 Features = Other OS|
CSM Support|Disabled|ADVANCED MODE > Boot > CSM Support = Disabled|
Secure Boot|Disabled|ADVANCED MODE > Boot > Secure Boot > Secure Boot = Disabled|
No. of CPU E-Cores Enabled|select higher number (ie. `4` if have following options: `1`, `2`, `3`, `4`)|ADVANCED MODE > Tweaker > Advanced CPU Settings > CPU Core Enabling Mode > No. of CPU E-Cores Enabled = maxNumber|if your CPU have E-Cores configure accordingly

</details>

<details><summary>

## 🍻[Multiboot with OpenCore](https://dortania.github.io/OpenCore-Multiboot/)
</summary>

🚀Set up a dual or triple boot with macOS Sequoia, Windows 11, and Ubuntu!(or Ubuntu Budgie!)

Dual or Triple boot methods|Pros|Cons
:----|:----|:----
Multiple OS on a Single Disk|Low Cost-effective|Low Space efficiency, Low Performance, Risk of data loss, Setup Complexity, OS Updates can sometimes affect the bootloaders of other OSes
Multiple OS on Different Disks|Improved performance, Data isolation for each OSes, Easier OS management, OSes removal Flexibility|High Cost

### Multiple OS on a Single Disk

> Backups: Crucial! Back up your important data before you begin.

#### Requirements:

- A Computers with pre-installed Windows 11

if you need follow: [Install Windows/ Linux using Android](https://github.com/arghya339/some-stupid-thing/blob/main/Install-Windows-Linux-using-Android.md)

#### Create Disks Partitions for each OSes:

- Open Windows `Disk Management`
- right click `Basic Disk (C:)`
- `Shrink Volume...`
- `Enter the amount of space to shrink in MB:` `131584` [Recommended: 128 GB (353300/ 131584 MB) or 256 GB (263168 MB) or ..more] [1024 MB = 1 GB]
  ```
  128 GB → Windows (128 GB × 1024 = 131,072 MB)
  (Toal size before shrink in MB - 131,072 MB) = Enter the amount of space to shrink in MB 
  Rest of disk → macOS
  ```
- `Shrink`
- `128.00 GB` `Unallocated`
  > Make sure Windows partition has enough space ie. 120/ 128 GB or more (Recommended)
- right click on Unallocated Space
- New Simple Volume...
- Next > Next > Next
- File system: `NTFS` Volume label: `Macintosh HD`
- Next > Finish.

#### Preparing

- macOS Sequoia Installer with EFI & macOS recovery files
- [Ubuntu](https://ubuntu.com/download/desktop) or [Ubuntu Budgie](https://ubuntubudgie.org/downloads/) ISO
- [Rufus](https://github.com/pbatard/rufus/releases)

#### Create Ubuntu Bootable USB

- Use a tool like Rufus to create a bootable USB drive with the Ubuntu ISO.

#### Install Ubuntu:

- Boot from the USB Drive, and follow the on-screen prompts. During installation, choose to `install Ubuntu alongside Windows`

#### Install macOS Sequoia

- Boot from the macOS Installer USB Drive
- After successfully boot into macOS recovery
- Open `Disk Utility` from macOS recovery > click on `View` > chose `Show All Devices` > select `Macintosh HD` partitions in `Internal` Disk > click on `Erase` > Name: `Macintosh HD` and Format: `APFS` > click on `Erase` > Done > now close `Disk Utility`.
- Install macOS: Follow the on-screen instructions to install macOS Sequoia on its dedicated SSD or partition (`128.00 GB` `Macintosh HD`).
- Copy OpenCore to your macOS Drive: After installing macOS, you'll need to copy OpenCore EFI form USB Drive to your macOS drive's EFI partition.

### Multiple OS on Different Disks

#### Requirements:

- A Computers with pre-installed Windows 11

if you need follow: [Install Windows/ Linux using Android](https://github.com/arghya339/some-stupid-thing/blob/main/Install-Windows-Linux-using-Android.md)

#### Drives:

- You'll need two or more drives for each OSes

#### Preparing

- macOS Sequoia Installer with EFI & macOS recovery files
- [Ubuntu](https://ubuntu.com/download/desktop) or [Ubuntu Budgie](https://ubuntubudgie.org/downloads/) ISO
- [Rufus](https://github.com/pbatard/rufus/releases)

#### Create Ubuntu Bootable USB

- Use a tool like Rufus to create a bootable USB drive with the Ubuntu ISO.

#### Install Ubuntu:

- Boot from the USB Drive, and follow the on-screen prompts. During installation, choose to `install Ubuntu`

#### Install macOS Sequoia

- Boot from the macOS Installer USB Drive
- After successfully boot into macOS recovery
- Open `Disk Utility` from macOS recovery > click on `View` > chose `Show All Devices` > select dedicated Disk > click on `Erase` > Name: `Macintosh HD` and Format: `APFS` > click on `Erase` > Done > now close `Disk Utility`.
- Install macOS: Follow the on-screen instructions to install macOS Sequoia on the dedicated drive
- Copy OpenCore to your macOS Drive: After installing macOS, you'll need to copy OpenCore EFI form USB Drive to your macOS drive's EFI partition.

> See [Windows GPU Selection](https://dortania.github.io/OpenCore-Install-Guide/extras/spoof.html#windows-gpu-selection) if you dual boot macOS alongside Windows & also have multiple dGPU on your System.

<details><summary>

### 🛸Removing Ubuntu or Sequoia from a dual/triple-boot setup with Windows 11 on a single disk
</summary>

#### Back Up Your Data:
- Before you begin, back up any important data from your Ubuntu or macOS Sequoia partition.

#### Open Disk Management

- Right click the `Windows` icon in the bottom left corner of your screen.
- select `Disk Management`.

#### Locate Ubuntu partitions:

- In the `Disk Management` window, you'll see a list of all partitions on your hard drive. Identify the partitions associated with `Ubuntu` (they might be labeled as `ext4` or have a large size).

#### Delete the Ubuntu partitions:

- from the `Disk Management` tool: Right-click on each Ubuntu partition and select `Delete Volume`.
- Confirm the deletion when prompted. This will erase all data on the Ubuntu partition(s), so make sure you have a backup.

#### Locate Sequoia partitions:

- from Disk Management: Look for a partition that doesn't have a drive letter assigned and is likely formatted with a file system that Windows doesn't recognize (e.g., `HFS+`, `APFS`). This is most likely your Hackintosh partition.

#### Delete the Sequoia partitions:

- Right-click on the Hackintosh partition and select `Delete Volume`. Confirm the deletion when prompted.

#### Extend your Windows partition:
- After deleting the `Ubuntu` or `macOS Sequoia` partitions, you'll have `unallocated space`.
- Right-click on your Windows partition (usually labeled as `C:`) and select `Extend Volume`.
- Follow the on-screen instructions to extend your Windows partition into the newly freed space.

#### Set Windows bootloader as the default

- Open `Command Prompt` as `administrator`: Type `cmd` in the `Start Menu` search bar.
- Right-click on `Command Prompt` and select `Run as administrator`.
- Use BCDEdit: In the Command Prompt window, type the following command and press `Enter`:

  ```
  bcdedit /set {bootmgr} path \EFI\microsoft\boot\bootmgfw.efi
  ```
> This command sets the `Windows bootloader` as the default.
#### Restart Your Computer

- Your computer should now boot directly into Windows 11 without the `GRUB bootloader` appearing.

#### Fix Bootloader Issues

- Boot from a `Windows 11 installation media` (USB drive).
- Select `Repair your computer`.
- Choose `Troubleshoot` -> `Advanced options` -> `Command Prompt`.
- In the `Command Prompt`, type the following commands, pressing `Enter` after each:

  ```
  bootrec /fixmbr
  ```

  ```
  bootrec /fixboot
  ```

  ```
  bootrec /rebuildbcd
  ```
- `Exit` Command Prompt and `Restart` your computer.

</details>
</details>

<details><summary>
    
## [💽Installation Process](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#installation-process)
</summary>

> [Understanding the macOS Boot Process with OpenCore](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/boot.html#opencore-booting)

### Boot from USB Drive

- Put `USB Drive` on target pc > `restart` your computer > press `F12` on keyboard > chose `USB Drive`
- chose `USB DRIVE (external) (dmg)` option by pick `1` 

### after sucessfully bootup to mac recovery

> Warning: Before erase disk make sure your computer able to connect internet. check internet access have or not: Open Safari > type apple.com in safari address bar & hit enter.

- select `Disk Uitility` > Continue > click on Disk Utility dropdown menu under view > Show all devices > now you can see all of your drive > chose your drive where you install macOS > click on Erase icon > Name: `Macintosh HD`, Format: `APFS`, Scheme: `GUID Partition Map` > click Erase > after erasing processing done close Disk Utility.
- connect to internet by connecting Ethernet or WiFi or Wireless USB Adapter or USB Tethering (if you are using USB Tethering using Android phone make sure you have [HoRNDIS.kext](https://github.com/jwise/HoRNDIS) and you change File Tranfer > USB Tethering)
- select `Install macOS Sequoia` > Continue > Agree > Agree > chose your drive that drive you recently formated (Macintosh HD) > Install > now chose `install macOS Sequoia (External)` form OpenCore boot menu > then chose `install macOS Sequoia (External)` form OpenCore boot menu > then chose `Macintosh HD` form OpenCore boot menu > then chose `Macintosh HD` form OpenCore boot menu > now setup your new Macintosh. 

### Moving OpenCore EFI from USB to macOS EFI Drive

#### Now you need to MOUNT your hidden EFI partition and copy USB Drive EFI folder to your EFI partition:

- Download [MountEFI.zip](https://github.com/corpnewt/MountEFI) and unzip it by left click
- right click and open `MountEFI.command` then click open again > ok > it download Python > now you can see MountEFI menu > mount `Macintosh HD(APFS)` drive by pick option `1` > then enter your password > then pick the USB Drive containing EFI folder for mycase USB Drive is called `USB Drive(FAT32)` so i pick option `3` > Pick the drive containing your system EFI for mycase new `EFI`(200MB+) so i pick option `1` > then enter your password > now quit form `mountEFI.command` press `Q` and hit `enter` > Now open `Folder` > Go > Computer > Macintosh HD > and also open USB Drive EFI folder from desktop > drag & drop EFI folder from USB Drive to Macintosh HD EFI folder > restart your Macintosh.

Alternative way to Mount your system EFI (Recommended): from MountEFI menu > Mount the Boot Drive's EFI by pick option `B` > then enter your password > close terminal > Terminate.

- [EFI-Agent](https://github.com/benbaker76/EFI-Agent/releases): GUI based tool to Mount Hidden EFI partitions, Alternative to MountEFI.cmd

download and Install EFI-Agent on mac > Open EFI-Agent > from macOS menu bar click on EFI-Agent logo
identifi macOS EFI partitions its typically something like:  `BSDName: disk0s1` `MountPoint: /Volumes/EFI` `VolumeName/DiskType: EFI`
after indentifi macOS EFI partitions > right click on macOS EFI chose `Mount`.
open Finder > Go > Computer
identify macOS EFI partitions its has same logo as Macintosh HD.
after identifi macOS EFI partitions from Finder > double click on macOS EFI partitions > double click on EFI folder
open your USB DRIVE by double click USB DRIVE from your Desktop folder > double click on USB DRIVE EFI folder
copy the USB DRIVE both BOOT and OC folder to macOS EFI folder
Now, you see macOS folder has following contents: Apple, BOOT, OC, in Computer > EFI > EFI dir.
Eject USB DRIVE form your Computer USB Port
Then, Restart your mac from Apple menu.

### 💐Congratulations! You have successfully built your first Hackintosh!

</details>

<details><summary>

## [⌨️USB Fixes by USB Mapping](https://dortania.github.io/OpenCore-Post-Install/usb/#macos-and-the-15-port-limit)
</summary>

[Hackintool](https://github.com/benbaker76/Hackintool/releases): Add USB port limit patch, Plug and unplug USB2.0 / USB3.0 devices and set port connector types then generate a `USBPorts.kext` & `SSDT-UIAC.aml`
</details>

## [ᯤIntel Wireless Module temp. fixes on Sequoia by OCLP](https://github.com/randomappleboi/Native-Wifi-for-Hackintoshes-with-Intel-Wireless-cards-on-macOS-sequoia)

<details><summary>

## 🛜Brodcom (BCM94360) WiFi Fixes by OCLP
</summary>

### Issues with OCLP Patch:
- macOS System Integrity Protection (SIP) permanet disabled by default: disabled FileVault (macOS's builtin drive encryption utility), `AMFIPass.kext` exist but some apps (ie. Adobe CC, Dropbox etc.) may crashed
- As `IOSkywalkFamily.kext` is Blocked, some intel ethernet may not work. Check ethernet by turning off WiFi. You may have to install additional kext if ethernet didn't work.

### After macOS installation,

#### Now you need to MOUNT your hidden EFI partition:

- Download [MountEFI.zip](https://github.com/corpnewt/MountEFI) and unzip it by left click
- right click and open `MountEFI.command` then click open again > ok > it download Python > now you can see MountEFI menu > Mount the Boot Drive's EFI by pick option `B` > then enter your password > close terminal > Terminate.

- [EFI-Agent](https://github.com/benbaker76/EFI-Agent/releases): GUI based tool to Mount Hidden EFI partitions, Alternative to MountEFI.cmd

#### Make some modifications, you can use the OC snapshot tool (Cmd/Ctrl + R) in [ProperTree](https://github.com/corpnewt/ProperTree) to update the `config.plist`:

Next, let's open ProperTree and edit our config.plist:

`ProperTree.command`

Once ProperTree is running, open your `config.plist` by pressing Cmd/Ctrl + O and selecting the config.plist file on your system boot drive's EFI.

After the config is opened, press Cmd/Ctrl + R and point it at your EFI/OC folder to perform a `OC Snapshot`.

#### Open `config.plist` and make the following changes:

Path|Quirk|Type|Value|Comment
:----|:----|:----|:----|:----
Root > Misc > Security|SecureBootModel|String|Disabled|
Root > NVRAM > Add > 7C436110-AB2A-4BBB-A880-FE41995C9F82|csr-active-config|Data|03080000|
Root > NVRAM > Delete > 7C436110-AB2A-4BBB-A880-FE41995C9F82|0|String|csr-active-config|to Disabling SIP

#### Add the following kexts to kext folder and include them in config.plist:

- Download following kexts

[OCLP WiFi Kexts](https://github.com/dortania/OpenCore-Legacy-Patcher/tree/main/payloads/Kexts/Wifi):
`IO80211FamilyLegacy.kext`
`AirPortBrcmNIC.kext`
`IOSkywalkFamily.kext`
[`AMFIPass.kext`](https://github.com/dortania/OpenCore-Legacy-Patcher/tree/main/payloads/Kexts/Acidanthera)
> Note: `IO80211FamilyLegacy.kext` & `AirPortBrcmNIC.kext` compressing in `IO80211FamilyLegacy.zip`

- Add following kexts in config.plist

`IO80211FamilyLegacy.kext`
`AirPortBrcmNIC.kext`
`AMFIPass.kext`

> Add this three kexts in config.plist > `Root > Kernel > Add`

> Note: `IO80211FamilyLegacy.kext` required for loads an older version of the framework to to apply OpenCoreLegacyPatching

`IOSkywalkFamily.kext`

> Add this one kext in config.plist > `Root > Kernel > Block`

> Note: `IOSkywalkFamily.kext` required for OpenCore to block that natively load the current IOSkywalk framework.

- then from ProperTree > File > Save (Ctrl+S)

#### `Clear NVRAM` form Open Core Boot Menu before booting into macOS:

reboot into open core boot menu chose `Clear NVRAM` then pick option `1`
> Note: to get Bluetooth working you need to Reset your NVRAM

#### Download and install [OC Legacy patcher](https://github.com/dortania/Opencore-Legacy-Patcher/releases/latest) and open OCLP click on `Post-Install Root Patch`. Give permissions when requested. then reboot system, WiFi will work after reboot.

#### Revert OCLP: Open `Open Core Legacy Patcher` and click on `Post-Install Root Patch` and revert patches.

</details>

<details><summary>

## [✉️Fixing iMessage & other iServices](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-imessage-and-other-services-with-opencore)
</summary>

Your Apple ID is the single most influential factor in using iServices.

If you have existing Apple products in your account, such as an iPhone, you should have no issues whatsoever using a generated serial set. However, if you recently created an account, that does not have any existing Apple hardware or App Store purchases, you may be required to call Apple once you have attemped logging in.

The following items will be created below and are required to use iServices:

 - MLB
 - ROM*
 - SystemProductName
 - SystemSerialNumber
 - SystemUUID

> Note: Sometime iServices required Wireless Adapter (WiFi) 

### Clean out old attempts

This is important for those who've tried setting up iMessage but failed, to start make sure your NVRAM has been cleared.

Next open terminal and run the following:

```sh
bash
sudo rm -rf ~/Library/Caches/com.apple.iCloudHelper*
sudo rm -rf ~/Library/Caches/com.apple.Messages*
sudo rm -rf ~/Library/Caches/com.apple.imfoundation.IMRemoteURLConnectionAgent*
sudo rm -rf ~/Library/Preferences/com.apple.iChat*
sudo rm -rf ~/Library/Preferences/com.apple.icloud*
sudo rm -rf ~/Library/Preferences/com.apple.imagent*
sudo rm -rf ~/Library/Preferences/com.apple.imessage*
sudo rm -rf ~/Library/Preferences/com.apple.imservice*
sudo rm -rf ~/Library/Preferences/com.apple.ids.service*
sudo rm -rf ~/Library/Preferences/com.apple.madrid.plist*
sudo rm -rf ~/Library/Preferences/com.apple.imessage.bag.plist*
sudo rm -rf ~/Library/Preferences/com.apple.identityserviced*
sudo rm -rf ~/Library/Preferences/com.apple.ids.service*
sudo rm -rf ~/Library/Preferences/com.apple.security*
sudo rm -rf ~/Library/Messages
```

### Cleaning up your AppleID
- Remove all devices from your AppleID: [Manage your devices](https://appleid.apple.com/account/manage)
= Enable 2 Factor-Auth
- Remove all iServices from Keychain, some examples:

```
ids: identity-rsa-key-pair-signature-v1
ids: identity-rsa-private-key
ids: identity-rsa-public-key
ids: message-protection-key
ids: message-protection-public-data-registered
ids: personal-public-key-cache
iMessage Encryption Key
iMessage Signing Key
com.apple.facetime: registrationV1
etc ...
```

> TIP
> Adding a payment card to the account and having a decent amount of purchases can also help. While not concrete, you can think of an AppleID as > a credit score where the better an Apple customer you are the more likely they won't have activation issues

### Serial Number Validity

Now enter the serial into the [Apple Check Coverage page](https://checkcoverage.apple.com/)

</details>

<details><summary>
    
## 🛰️Fix Location Accuracy in Hackintosh
</summary>

- fix Location accuracy in Hackintosh:
  - Location Service work without GPS, 
    - if you are connected to internet your internet service provide a location based public ip address, this ip address can be use as detect your computer location. this location accuracy very low compare to WiFi AP locations.
    - if you are using WiFi, WiFi scanning can detect nearby WiFi Access Points by MAC addresses and Received Signal Strength, this WiFi APs data send to Apple/Google WiFi location database using internet to compares both the detected APs & Apple/Google WiFi location database and finaly receved your WiFi AP locations. this location accuracy very low compare to GPS locations and depand on nearby WiFi dencity.
  - also you can connect USB GPS reciver to output NMEA data and process this data using GPS utilities like GPSD to get GPS loacation, aditionaly GPSD can be distribute GPS data to multiple applications like [QGIS](https://www.qgis.org/download/), [Apple Maps](https://beta.maps.apple.com/) do not directly support reading location data from GPSD. Unfortunately, Apple Maps does not natively support external GPS devices.
 
USB GPS|communication protocols|Official Driver|Third-Party Drivers
:----|:----|:----|:----
GlobalSat BU-353-S4|NMEA|[BU-353S4](https://www.globalsat.com.tw/en/a4-10593/BU-353S4.html)|[GPSD](https://formulae.brew.sh/formula/gpsd#default)/ [GPXSee](https://sourceforge.net/projects/gpxsee/files/Mac%20OS%20X/)/ [KisMac2](https://igrsoft.com/beta/KisMac2.zip)/ [QGIS](https://qgis.org/download/)/ [OpenCPN](https://opencpn.org/OpenCPN/info/downloadopencpn.html)
</details>

<details><summary>
    
## ✨Fix Keyboard RGB Support in macOS
</summary>

Keyboard OpenRGB Support fixed by flashing custom firmware

### Advantage and Disadvatage of flashing custom fimware:
- if your keyboard not supportd by OpenRGB, and if you are using openRGB on your keyboard your keyboard may frizz and keyboard MicroConroller may not connect your computer using UART portocol over USB. if you flash suppored custom firmware you can use OpenRGB without issue.
- when you apply openRGB effect on your suppored keyboard this effect very poortly sync to your keyboard, and this can bicked your keyboard MCU. you can fix it by flashing custom firmware
- some keyboard store rgb effect on keybord MicroController ESPROM this is potentially drastically shorten the life of your MCU. you can store settings (RGB effect) on OpenRGB software by flashing custom firmware
- flashing different keyboard firmware can bicked your keyboard

### [Install Instructions](https://sonixqmk.github.io//SonixDocs/install/#42-entering-bootloader-mode)

### Identify keyboard MCU:

- Redragon Kumara K552 has `EVision Sonix SN32F248B` MicroController

- ROYAL KLUDGE RK84 has `Sinowealth 8051 based BYK916 (SH68F90A)` MicroController and Wireless MCU: BK3632 (supports BT5.0 and 2.4GHz) 

- Redragon Fizz K617 has `Sinowealth 8051 based BYK916 (SH68F90A)` MicroController

- Portronics Hydra 10 has `Sinowealth 8051 based BYK916 (SH68F90A)` MicroController and Wireless MCU: BK3632 (supports BT5.0 and 2.4GHz)

### [Download](https://browse.qmk.fm/) Pre-Compile firmware:

[qmk_firmware for Redragon Kumara K552-RGB](https://github.com/SonixQMK/qmk_firmware/actions) github workflow name `[redragon/k552/rev2]` branch `sn32_master` then download `Pre-Compiled Firmware` file

[smk for Redragon Fizz K617](https://github.com/carlossless/smk/actions)

### Compile Firmware:

#### Prepare Your Build Environment:

- Install Homebrew: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

- Install QMK CLI: `brew install qmk/qmk/qmk`

#### Setting up QMK Enviroment:

`qmk setup SonixQMK/qmk_firmware -b sn32_master`

#### Compiling your keyboard firmware:

- command format to compile: `qmk compile -kb <keyboard> -km <keymap>`

- build Redragon K552-RGB firmware: `qmk compile -kb redragon/k552/rev2 -km default`

- build Redragon K552-Rainbow firmware: `qmk compile -kb redragon/k552/rev1 -km default`

### Download Flash Tool:

- [sonix-flasher](https://github.com/SonixQMK/sonix-flasher/releases): flash tools for Sonix MCU based keyboard

- [sinowealth-kb-tool](https://github.com/carlossless/sinowealth-kb-tool/releases): flash tool for Sinowealth MCU based keyboard

- [QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases): flashing tools collection, auto detects keyboard MCU & auto flash firmware

- [USB_MCU_ISP_Tool](https://www.sonix.com.tw/article-en-4336-30356): USB MicroControllerUnit InSystemProgress Tool is a official flash tool for Sonix MCU based keyboard

### Backup Keyboard ISP-firmware

Sonix Flasher > "Download Stock Firmware"

> Backups: Before flashing any custom firmware, it's highly recommended to create a backup of your keyboard's original firmware, just in case you need to revert back.

#### Backup Keyboard ISP-firmware using [stlink](https://github.com/stlink-org/stlink/releases) (Alternative):

### identify USB keyboard VID and PID using zadig (Alternative):

[zadig.exe](https://github.com/pbatard/libwdi/releases)

open zadig and chose usb devices > USB ID: `USB ID`'s first is `VID` and second one is `PID` and ignore third one.

### Entering Bootloader mode:

Sonix Flasher > "Reboot to Bootloader"

#### Put your keyboard into bootloader mode (Alternative)

- Disconnect the keyboard from your computer.

- Press and hold the `Esc` key and the `Fn` key simultaneously.

- While holding these keys, reconnect the keyboard to your computer.

- Continue holding the keys for a few seconds until the keyboard enters bootloader mode.

### Flash custom firmware:



### Flash custom firmware (Alternative):

open firmware flash tools based on your keyboard

fill VID and PID form zadig tools

chose custom firmware file based on keyboard you have

if you have Redragon kumara k552-RGB chose `SN32F240B` from chip list ok and  chose `redragon_k552_rev2.bin` firmware file from extracted folder

if you have Redragon Fizz K617 chose `E-YOOSO Z11.HEX`

### Unplug and replug your keyboard:

- Once the flashing is done, unplug the USB cable from your keyboard. Plug it back in.
- Your keyboard should now be running the QMK firmware.

### Restore keyboard ISP-firmware:

Sonix Flasher > "Revert to Stock Firmware"

### Download RGB Tools:

- [OpenRGB](https://gitlab.com/CalcProgrammer1/OpenRGB/-/releases)
- [KeyboardVisualizer.exe](https://gitlab.com/CalcProgrammer1/KeyboardVisualizer/-/releases)
- [Aurora-RGB.exe](https://github.com/Aurora-RGB/Aurora/releases)

</details>

<details><summary>

## 🗨️Commonly Asked Some Stupid Questions 
</summary>

¹@myStupidMind: Apple Maps Support External GPS Receiver?

--> @apple: NO

²@myStupidMind: Logitech Brio Webcam has infrared camera it support `Windows Hello` can I use as `macOS FaceID` for biometric login

--> @apple: NOO

³@myStupidMind: Kensington VeriMark USB Fingerprint Key Reader support `Windows Hello` with `FIDO U2F` Security, it can be used as `macOS TuchID`?

--> @apple: NOOO

⁴@myStupidMind: Apple Magic Keyboard has built in `TuchID` it support Apple Silicon (M1/M2/M3/M4) Arm Mac so possible to work on Intel x86 Mac?

--> @apple: NOOOO

</details>

<details><summary>
    
## 🔋[Upgrade Hackintosh](https://dortania.github.io/OpenCore-Post-Install/universal/update.html#updating-opencore)
</summary>

to update or upgrade your hackintosh
- if you using old GPU like me, make sure GPU supported for Update
- [AppleALC.kext](https://github.com/acidanthera/AppleALC) is broken because AppleHDA.kext was removed from macOS Tahoe. Use HDMI/DP audio for the time being.
- Please Disabled [BluetoolFixup.kext](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) during macOS Sequoia update, otherwise its causes kernel panics.
- Please Disabled [IntelBTPatcher.kext](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/tree/master/IntelBTPatcher) during macOS Tahoe update, otherwise its causes kernel panics.
- [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen) is bugged on AMD RX 6XXX Series cards in macOS Tahoe, so you can't use boot arguments like `agdpmod=pikera`.
- [IntelMausi.kext](https://github.com/acidanthera/IntelMausi) may not work correctly with certain Intel ethernet chipsets in macOS Tahoe.
- if you trying to upgrade your hackintosh with latest one make sure your `SystemProductName` support latest macos if not try this: ie. latest [macosSequoia](https://www.apple.com/in/macos/) supported device list include `iMac2019(iMac19,1)` so make sure your system hidden `EFI` > `OC` > `config.plist` > `Root` > `PlatformInfo` > `Generic` > `SystemProductName` set to `iMac19,1` (note: to modify config.plist in your system hidden EFI you need mountEFI program to mount your system hidden EFI).
- if you change `SystemProductName` to upgrade your hackintosh make sure you also update `SerialNumber` that match with `SystemProductName`, to do this you need [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to genarate specific SMBIOS data for your system other wise you may not acess iServices.
- Restart your hackintosh
- Rebuild `EFI` form scratch for your system (rebuild EFI using latest OpenCore & download latest requred kext and add to Kexts folder under OC under EFI)
- Replace the OpenCore files with the ones you just downloaded
  - The important ones to update:
    - EFI/BOOT/BOOTx64.efi
    - EFI/OC/OpenCore.efi
    - EFI/OC/Drivers/OpenRuntime.efi (Don't forget this one, OpenCore will not boot with mismatched versions)
> You can also update other drivers you have if present, these are just the ones that must be updated in order to boot correctly
- then follow [Moving OpenCore EFI from USB to macOS EFI Drive](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md#moving-opencore-efi-from-usb-to-macos-efi-drive) Guide
- then upgrade your mac using `System Preferences > Software Update` (Recommended) or App Store.
- then reboot your system
</details>

<details><summary>

## 📊[Cinebench](https://www.maxon.net/en/downloads/cinebench-2024-downloads) / [Geekbench](https://www.geekbench.com/download/) Score
</summary>

- Hardware i have:

  - GIGABYTE B660M DS3H AX DDR4 (rev. 1.2)
  - Intel Core i3-12100F (with Intel Laminar RM1 Cooler)
  - Cooler Master MasterGel Regular
  - G.SKILL Ripjaws 8GB DDR4 3200MHz
  - WD Blue SN570 NVMe SSD 500 GB
  - MSI MAG FORGE 100M
  - SAPPHIRE PULSE RADEON RX 550 4GB GDDR5 (Lexa)
  - Corsair CV450
  - Acer Nitro VG240YB 23.8 Inch, FHD 75Hz
  - Dell KB216 Multimedia Wired Keyboard (plaining for replace this keyboard with Redragon Kumara K552 in future)
  - Zebronics Zeb-Transformer-M - Premium Gaming Mouse

<details><summary>
[windows-me](https://github.com/arghya339/some-stupid-thing/blob/main/Install-Windows-Linux-using-Android.md#rcomended-apps)
</summary>

- [GIGABYTE APP Center](https://www.gigabyte.com/Motherboard/B660M-DS3H-AX-DDR4-rev-1x/support#Support-Utility)
- [Gigabyte SIV](https://www.gigabyte.com/Motherboard/B660M-DS3H-AX-DDR4-rev-1x/support#Support-Utility)
- [Gigabyte @Bios.exe](https://www.gigabyte.com/Motherboard/B660M-DS3H-AX-DDR4-rev-1x/support#Support-Utility) (APP Center > LiveUpdate > Recommend installation > New Utilities > @Bios.exe)
- [Gigabyte RGB Fusion](https://www.gigabyte.com/Motherboard/B660M-DS3H-AX-DDR4-rev-1x/support#Support-Utility)
- [Realtek Audio Console](https://apps.microsoft.com/detail/9P2B8MCSVPLN)
- [AMD Software: Adrenalin Edition](https://www.amd.com/en/support/downloads/drivers.html/graphics/radeon-600-500-400/radeon-rx-500-series/radeon-rx-550.html)
- [SANDISK Dashboard](https://support-en.sandisk.com/app/products/downloads/softwaredownloads)
- [Acer Display Widget](https://www.acer.com/in-en/acer-display-widget) / [Monitorian](https://apps.microsoft.com/detail/9NW33J738BL0)
</details>

- Benchmark Score my macine gain:

<details><summary>
Cinebench
</summary>
    
Cinebench is an industry-standard benchmarking software

- Chinebench version: 2024

OS|OS Version|CPU Single Core|CPU Multi Core|GPU|Chinebench version
:----|:----|:----|:----|:----|:----  
Windows 10 Pro|||||
Windows 11 Pro|25H2|i3-12100F dont have iGPU Failed|i3-12100F dont have iGPU Abort|AMD Radeon RX 550 Not Supported|2024
MacOS Monterey 12|||||
macOS Ventura 13|||||
macOS Sonoma 14|14.7.3|i3-12100F dont have iGPU Failed|i3-12100F dont have iGPU Abort|AMD Radeon RX 550 Not Supported|2024
MacOS Sequoia 15|||||
Ubuntu|||||

</details>

Geekbench is an cross-platform benchmarking software

- Geekbench version: 6

OS|OS Version|CPU Single-Core|CPU Multi-Core|GPU OpenCL|GPU Vulkan/Metal|Geekbench version
:----|:----|:----|:----|:----|:----|:----
Windows 10 Pro|22H2|2264|6588|11763|12551|6.5.0
Windows 11 Pro|25H2|2267|6324|11140|13087|6.5.0
macOS Monterey 12|12.7.6|2222|6547|10511|11851|6.5.0
macOS Ventura 13|13.7.8|2196|6534|10601|12825|6.5.0
macOS Sonoma 14|14.8.3|2217|6511|13357|17429|6.5.0
macOS Sequoia 15|15.7.3|2190|6459|13354|17490|6.5.0
macOS Tahoe 26||||||
Ubuntu|24.04.3|1815|6742|8361|14587|6.5.0
```
sudo apt install mesa-opencl-icd -y  # install opencl driver
```
```
cd $HOME/Downloads/Geekbench-*-Linux && ./geekbench6 --gpu OpenCL  # run opencl benchmark
```
```
sudo apt install mesa-vulkan-drivers  # install vulkan driver
```
```
~/Downloads/Geekbench-*-Linux/geekbench6 --gpu vulkan  # run vulkan benchmark
```
```
sudo apt install gddccontrol -y
```

</details>

<details><summary>

## 💡Rcomended Apps
</summary>

AI

- [ChatGPT](https://github.com/lencx/ChatGPT/releases): get instant answers and inspiration
- [chatbox](https://chatboxai.app/install?download=darwin-x86_64): User-friendly Desktop Client App for AI Models ([Chat GPT](https://platform.openai.com/), [Gemini](https://aistudio.google.com/apikey), [DeepSeek](https://platform.deepseek.com/)-[Docs](https://github.com/deepseek-ai/awesome-deepseek-integration/blob/main/docs/chatbox/README.md))
- [Microsoft Copilot](https://apps.apple.com/us/app/microsoft-copilot/id6738511300): OpenAI and Microsoft AI models.

  <details><summary>
  Run DeepSeek Locally
  </summary>

  we can use [DeepSeek-R1-Distill-Qwen-14B](https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Qwen-14B) (coding and mathematics) for run deepseek locally, for more info see: [DeepSeek-R1-Distill Models](https://github.com/deepseek-ai/DeepSeek-R1?tab=readme-ov-file#deepseek-r1-distill-models)

  Install Homebrew (if you haven't already):

  ```sh
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
  ```

  Check if Homebrew was installed successfully:
  ```
  brew --version
  ```

  Install Python 3:
  ```
  brew install python
  ```

  Verify Python 3 installation
  ```
  python3 --version
  ```

  Update pip
  ```
  pip install --upgrade pip
  ```

  Install Python requirements.txt
  ```
  pip install -r requirements.txt
  ```

  Install git for clone DeekSeek:
  ```
  brew install git
  ```

  Clone the [DeepSeek-R1-Distill-Qwen-14B](https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Qwen-14B) Repository
  In your terminal, run:
  ```
  git clone https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Qwen-14B
  ```
  ```
  cd DeepSeek-R1-Distill-Qwen-14B
  ```

  Install Miniconda
  ```
  brew install --cask miniconda
  ```
  Initialize Conda
  ```
  conda init zsh
  ```
  reload the Zsh configuration
  ```
  source ~/.zshrc
  ```

  Install PyTorch
  ```
  conda install pytorch -c pytorch
  ```

  Create virtual env
  ```
  python3 -m venv .venv
  ```

  Active venv
  ```
  source .venv/bin/activate
  ```

  Install Torch, Transformers, ...
  ```
  pip install torch transformers accelerate safetensors
  ```
  Install PyTorch for CPU-only:
  Since our system does not support GPU acceleration via CUDA for the AMD GPU, you need to install PyTorch that works with CPU (PyTorch primarily supports NVIDIA GPUs for CUDA):

  ```
  pip install torch==1.12.1
  ```

  Load DeepSeek-R1-Distill-Qwen-14B Model in Python using Transformers

  ```
  cd DeepSeek-R1-Distill-Qwen-14B
  ```
  ```
  touch chatbot.py
  ```
  ```
  nano chatbot.py
  ```
  
  code to load the model
  
  ```py
  import torch
  from transformers import AutoModelForCausalLM, AutoTokenizer

  # Replace with your actual model directory.
  model_path = "os.path.expanduser("~/DeepSeek-R1-Distill-Qwen-14B")"

  # Use Auto classes to load the model and tokenizer
  tokenizer = AutoTokenizer.from_pretrained(model_path)
  model = AutoModelForCausalLM.from_pretrained(model_path, trust_remote_code=True) # trust_remote_code might be needed depending on model

  # Move the model to the CPU
  model.to("cpu")

  # Example text generation
  prompt = "Translate to French: Hello, world!"
  input_ids = tokenizer(prompt, return_tensor="pt").input_ids.to("cpu")

  with torch.no_grad():
    output = model.generate(input_ids, max_length=50)  # Adjust max_length as needed

  generated_text = tokenizer.decode(output[0], skip_special_tokens=True)
  print(generated_text)

  ```
  paste this code in nano text editor > `Ctrl+X` > `y` > `Enter`.

  run following command
  ```
  python3 chatbot.py
  ```

  Create a Chatbot API using Flask:
  Now that you've loaded the model, you need to create a web server to handle communication with the chatbox.dmg (the GUI application) or any 
  other frontend. Flask is a lightweight Python web framework that’s perfect for this.
  Install Flask:

  ```
  pip install Flask
  ```

  Create chatbot_app.py to serve as the backend for your chatbot:

  ```py
  from flask import Flask, request, jsonify
  from transformers import AutoModelForCausalLM, AutoTokenizer

  # Load the model and tokenizer
  model_name = "path_to_deepseek_model_or_huggingface_model"
  tokenizer = AutoTokenizer.from_pretrained(model_name)
  model = AutoModelForCausalLM.from_pretrained(model_name)

  # Initialize Flask app
  app = Flask(__name__)

  @app.route("/chat", methods=["POST"])
  def chat():
    user_input = request.json.get("message")  # Extract the message from the request
    
    # Tokenize input and generate a response
    inputs = tokenizer(user_input, return_tensors="pt")
    outputs = model.generate(inputs["input_ids"])

    # Decode the response and return as JSON
    bot_response = tokenizer.decode(outputs[0], skip_special_tokens=True)
    return jsonify({"response": bot_response})

  if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0", port=5000)
  ```

  This Flask server listens for POST requests at /chat and returns a generated response from the DeepSeek-R1-Distill-Qwen-14B model.
  Run Flask App:
  ```
  python3 chatbot_app.py
  ```

  Integrating with chatbox.dmg:
  Check how chatbox.dmg communicates:

  chatbox.dmg allows for external communication (via HTTP API calls or WebSocket), you can connect it to the Flask API by sending HTTP 
  requests to `http://localhost:5000/chat`.

  Configure chatbox.dmg:
  chatbox.dmg supports custom configurations for API calls, provide it with the API endpoint (`http://localhost:5000/chat`) for sending messages 
  and receiving responses from the Flask server.

  Note: Qwen-14B Model is a large Size, and running it on our setup (Hackintosh) might be slow.
  </details>
  
- [diffusionbee-stable-diffusion-ui](https://github.com/divamgupta/diffusionbee-stable-diffusion-ui/releases): fastest and easiest toolbox to run Creative Al Tools locally

Audio

- [Soundflour](https://github.com/mattingalls/Soundflower/releases): MacOS system extension that allows applications to pass audio to other applications.
- +[SoundflourBed](https://github.com/mLupine/SoundflowerBed/releases): SoundflowerBed is an application that resides in the menu bar allowing you to tap into Soundflower channels and route them to an audio device.
- [BlackHole](https://github.com/ExistentialAudio/BlackHole#installation-instructions): modern macOS audio loopback driver that allows applications to pass audio to other applications with zero additional latency, alternative to SoundFlower.

   <details><summary>
   Set Up an Multi-Output Device with BlackHole
   </summary>

   - Install Homebrew if you not already installed open macOS Terminal and enter following command:
     ```
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ```

   - Install BlackHole 2 chennel (if you have 2 speaker based audio output device) using brew:
   ~ `brew install blackhole-2ch`

   - Open `Audio MIDI Setup` app from macOS LounchPad > Others > Audio MIDI Setup
   - Create Devices (`+`) > `Create Multi-Output Device` > Select: ✅ BlackHole 2ch ✅ Acer VG240Y (HDMI) (Acer VG240Y is my Monitor with 2x2w 
     speaker, so select your Audio Output device)
   - select `Multi-Output Device` as  Audio from macOS control center.
   - Now you should be able to control HDMI/DP audio via keyboard dedicated media key and listen audio via HDMI/DP Port.
   </details>

- [BackgroundMusic](https://github.com/kyleneideck/BackgroundMusic/releases): Per-application volume control
- [eqMac](https://github.com/bitgapp/eqMac/releases): macOS System-wide Audio Equalizer & Volume Mixer
- [audacity](https://github.com/audacity/audacity/releases): Audio Editor, Alternative to Apple Logic Pro
- [GarageBand](https://apps.apple.com/in/app/garageband/id682658836?ls=1&mt=12): easiest way to create a great-sounding song on your Mac

Browser

- [Chromium](https://formulae.brew.sh/cask/chromium): [Latest Chromium download](https://github.com/arghya339/crdl)
- [Chrome](https://www.google.com/chrome/): Google [Chromium](https://github.com/chromium/chromium). [Microsoft Edge](https://apps.apple.com/us/app/microsoft-edge-ai-browser/id1288723196) / [TestFlight](https://apps.apple.com/us/app/testflight/id899247664?platform=iphone)+[joinMicrosoftEdgeBeta](https://testflight.apple.com/join/JkU2rh21): Extensions supported Chromium based iOS Browser, better than [Chrome](https://apps.apple.com/us/app/google-chrome/id535886823). [Chromium](https://github.com/arghya339/crdl): Extensions supported Chromium based Android Browser, better than [Chrome](https://play.google.com/store/apps/details?id=com.android.chrome)

  <details><summary>
  Top 50 Chrome Extensions
  </summary>    
 
  - [Chrome Web Store Launcher (by Google)](https://chromewebstore.google.com/detail/chrome-web-store-launcher/gecgipfabdickgidpmbicneamekgbaej): provides quick, easy access to all your Chrome Extensions.
  - [uBlock Origin](https://chromewebstore.google.com/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm): an efficient ads blocker.
  - [Popup Blocker (strict)](https://chromewebstore.google.com/detail/popup-blocker-strict/aefkmifgmaafnojlojpnekbpbmjiiogg): Strictly block all popup requests from any website.
  - [AdGuard VPN](https://chromewebstore.google.com/detail/adguard-vpn-%E2%80%94-free-secure/hhdobjgopfphlmjbmnpglhfcgppchgje): free & secure proxy for Chrome.
  - [Proton VPN](https://chromewebstore.google.com/detail/proton-vpn-fast-secure/jplgfhpmjnbigmhklmmbgecoobifkmpa): Secure your internet and protect your online privacy in one click.
  - [User-Agent Switcher and Manager](https://chromewebstore.google.com/detail/user-agent-switcher-and-m/bhchdcejhohfmigjafbampogmaanbfkg): Spoof websites trying to gather information about your web  Browser.
  - [Buster](https://chromewebstore.google.com/detail/buster-captcha-solver-for/mpbjkejclgfgadiemmefgebjfooflfhl): Captcha Solver for Humans.
  - [floccus](https://chromewebstore.google.com/detail/floccus-bookmarks-sync/fnaicdffflnofjppbagibeoednhnbjhg): bookmarks sync.
  - [TabCloud](https://chromewebstore.google.com/detail/tabcloud/npecfdijgoblfcgagoijgmgejmcpnhof): Save and restore window sessions over time and across multiple Browser.
  - [Bitwarden](https://chromewebstore.google.com/detail/bitwarden-password-manage/nngceckbapebfimnlniiiahkandclblb): Password Manager.
  - [Proton Pass](https://chromewebstore.google.com/detail/proton-pass-free-password/ghmbeldphafepmbegfdlkpapadhbakde): FOSS Password Manager, Alternative to `Bitwarden`.
  - [Google Translate](https://chromewebstore.google.com/detail/google-translate/aapbdbdomjkkjkaonfhkkikfgjllcleb): View translations easily as you browse the web.
  - [Absolute Enable Right Click & Copy](https://chromewebstore.google.com/detail/absolute-enable-right-cli/jdocbkpgdakpekjlhemmfcncgdjeiika): Force Enable Right Click & Copy.
  - [UltraWideo](https://chromewebstore.google.com/detail/ultrawideo/bfbnagnphiehemkdgmmficmjfddgfhpl): that manipulates video aspect ratio to fit your entire screen.
  - [~~Search by Image~~](https://chromewebstore.google.com/detail/search-by-image/cnojnbdhbhnkbcieeekonklommdnndci): A powerful reverse image search tool, with support for various search engines, such as Google, Bing, Yandex, Baidu and TinEye.
  - [Redirect AMP to HTML](https://chromewebstore.google.com/detail/redirect-amp-to-html/kifkmmpiicbcnkjaliilaoeaojlldonl): Automatically redirects AMP pages to their canonical HTML equivalent.
  - [AI Grammar Checker & Paraphraser](https://chromewebstore.google.com/detail/ai-grammar-checker-paraph/oldceeleldhonbafppcapldpdifcinji): Instantly Enhance Your Texts with this.
  - [BlockSite](https://chromewebstore.google.com/detail/blocksite-block-websites/eiimnmioipafcokbfikbljfdeojpcgbh): Block Websites.
  - [ChatGPT for Google](https://chromewebstore.google.com/detail/chatgpt-for-google/jgjaeacdkonaoafenlfkkkmbaopkbilf): Display ChatGPT response alongside search engine results.
  - [ClearURLs](https://chromewebstore.google.com/detail/clearurls/lckanjgmijmafbedllaakclkaicjfmnk): Remove tracking elements from URLs.
  - [Cookie AutoDelete](https://chromewebstore.google.com/detail/cookie-autodelete/fhcgjolkccmbidfldomjliifgaodjagh): Automatically delete unwanted cookies from your closed tabs while keeping the ones you want.
  - [Dark Reader](https://chromewebstore.google.com/detail/dark-reader/eimadpbcbfnmbkopoojfekhnkhdbieeh): Dark mode for every website.
  - [Don't F*** With Paste](https://chromewebstore.google.com/detail/dont-f-with-paste/nkgllhigpcljnhoakjkgaieabnkmgdkb): Prevents the blocking of copying from & pasting into input fields.
  - [Enhancer for YouTube™](https://chromewebstore.google.com/detail/enhancer-for-youtube/ponfpcnoihfmfllpaingbgckeeldkhle): Take control of YouTube and boost your user experience!
  - [Firefox Relay](https://chromewebstore.google.com/detail/firefox-relay/lknpoadjjkjcmjhbjpcljdednccbldeb): Firefox Relay makes it easy to create email masks that forward to your true inbox.
  - [Google Analytics Opt-out Add-on (by Google)](https://chromewebstore.google.com/detail/google-analytics-opt-out/fllaojicojecljbmefodhfapmkghcbnh): Tells the Google Analytics JavaScript not to send information to Google Analytics.
  - [Google Keep Chrome Extension](https://chromewebstore.google.com/detail/google-keep-chrome-extens/lpcaedmchfhocbbapmcbpinfpgnhiddi): Save to Google Keep in a single click!
  - [Keepa](https://chromewebstore.google.com/detail/keepa-amazon-price-tracke/neebplgakaahbhdphmkckjjcegoiijjo): Amazon Price Tracker.
  - [Offline QR Code Generator](https://chromewebstore.google.com/detail/offline-qr-code-generator/fehmldbcmhbdkofkiaedfejkalnidchm): Generate QR codes for the current tab URL.
  - [Honey](https://chromewebstore.google.com/detail/honey-automatic-coupons-r/bmnlcjabgnpnenekpadlanbbkooimhnj): Automatic Coupons Find.
  - [Picture-in-Picture Extension (by Google)](https://chromewebstore.google.com/detail/picture-in-picture-extens/hkgfoiooedgoejojocmhlaklaeopbecg): Watch video using Picture-in-Picture.
  - [Privacy Test](https://chromewebstore.google.com/detail/privacy-test/pdabfienifkbhoihedcgeogidfmibmhp): Checks whether you have enhanced private data protection and prevents tracking of your on-line activity.
  - [Read Aloud](https://chromewebstore.google.com/detail/read-aloud-a-text-to-spee/hdhinadidafjejdhmfkjgnolgimiaplp): A Text to Speech Voice Reader.
  - [Return YouTube Dislike](https://chromewebstore.google.com/detail/return-youtube-dislike/gebbhagfogifgggkldgodflihgfeippi): Returns ability to see dislikes.
  - [Save to Google Drive](https://chromewebstore.google.com/detail/save-to-google-drive/gmbmikajjgmnabiglmofipeabaddhgne): Save web content or screen capture directly to Google Drive.
  - [Scroll To Top](https://chromewebstore.google.com/detail/scroll-to-top/hegiignepmecppikdlbohnnbfjdoaghj): Scroll to top and vice versa in a window.
  - [Seedr](https://chromewebstore.google.com/detail/seedr/abfimpkhacgimamjbiegeoponlepcbob): Download and play Torrent Seeding.
  - [SponsorBlock for YouTube](https://chromewebstore.google.com/detail/sponsorblock-for-youtube/mnjggcdmjocbbbhaepdhchncahnbgone): Skip Sponsorships.
  - [Tampermonkey](https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo): userscripts manager.
  - [Temp Mail](https://chromewebstore.google.com/detail/temp-mail-disposable-temp/inojafojbhdpnehkhhfjalgjjobnhomj): Disposable Temporary Email.
  - [Thumbnail Rating Bar for YouTube™](https://chromewebstore.google.com/detail/thumbnail-rating-bar-for/cmlddjbnoehmihdmfhaacemlpgfbpoeb): Displays a rating bar (likes/dislikes) on the bottom of every YouTube™ video thumbnail.
  - [uBlacklist](https://chromewebstore.google.com/detail/ublacklist/pncfbmialoiaghdehhbnbhkkgmjanfhe): Blocks sites you specify from appearing in Google search results.
  - [Unhook](https://chromewebstore.google.com/detail/unhook-remove-youtube-rec/khncfooichmfjbepaaaebmommgaepoid): Remove YouTube Recommended.
  - [Url Shortener](https://chromewebstore.google.com/detail/url-shortener/oodfdmglhbbkkcngodjjagblikmoegpa): The best way to create short links using TinyUrl.
  - [Video Resumer](https://chromewebstore.google.com/detail/video-resumer/bongjkoajofkfpofginnhecihgaeldpe): Automatically resumes YouTube videos from where you played them last.
  - [Video Roll](https://chromewebstore.google.com/detail/video-roll-all-in-one-vid/cokngoholafkeghnhhdlmiadlojpindm): Rotate watching video.
  - [WA Web Plus by Elbruz Technologies](https://chromewebstore.google.com/detail/wa-web-plus-by-elbruz-tec/ekcgkejcjdcmonfpmnljobemcbpnkamh): Add more tools and options for WhatsApp Web for more privacy and reliability.
  - [WOT](https://chromewebstore.google.com/detail/wot-website-security-safe/bhmmomiinigofkjcapegjjndpbikblnp): Website Security & Safety Checker.
  </details>

- [FireFox](https://www.mozilla.org/en-US/firefox/mac/): Firefox, is a free and open source web browser that puts your privacy first. + [Top 50 Firefox Extensions](https://addons.mozilla.org/en-US/firefox/collections/17182101/top-50/): by arghya
- [Brave](https://brave.com/en-in/download/): Browser built with BAT based on Ethereum cryptocurrencies network, built in AdBlocker & Tor, support Chrome Extensions, better than [Chrome](https://play.google.com/store/apps/details?id=com.android.chrome).
- [Tor Browser](https://www.torproject.org/download/): Protect yourself against tracking, surveillance, and censorship.
- [Microsoft Edge](https://www.microsoft.com/en-us/edge/download): smarter way to browse, Chromium based, support crx extensions in Desktop, [Android](https://play.google.com/store/apps/details?id=com.microsoft.emmx.canary) & [iOS](https://apps.apple.com/us/app/microsoft-edge-ai-browser/id1288723196), better than [Chrome](https://play.google.com/store/apps/details?id=com.android.chrome).

  <details><summary>
  Top 50 Edge Extensions
  </summary>    
 
  - [Chrome Web Store Launcher (by Google)](https://chromewebstore.google.com/detail/chrome-web-store-launcher/gecgipfabdickgidpmbicneamekgbaej): provides quick, easy access to all your Chrome Extensions.
  - [uBlock Origin](https://microsoftedge.microsoft.com/addons/detail/ublock-origin/odfafepnkmbhccpbejgmiehpchacaeak): an efficient ads blocker.
  - [Popup Blocker (strict)](https://microsoftedge.microsoft.com/addons/detail/popup-blocker-strict/ijhfkkgjgpcplfeajghagkcebakjcpge): Strictly block all popup requests from any website.
  - [AdGuard VPN](https://microsoftedge.microsoft.com/addons/detail/adguard-vpn-%E2%80%94-free-secu/bkcoaehlnhbggcbmohegigjfgfdiihmp): free & secure proxy for Chrome.
  - [Proton VPN](https://chromewebstore.google.com/detail/proton-vpn-fast-secure/jplgfhpmjnbigmhklmmbgecoobifkmpa): Secure your internet and protect your online privacy in one click.
  - [User-Agent Switcher and Manager](https://microsoftedge.microsoft.com/addons/detail/useragent-switcher-and-m/cnjkedgepfdpdbnepgmajmmjdjkjnifa): Spoof websites trying to gather information about your web  Browser.
  - [Buster](https://microsoftedge.microsoft.com/addons/detail/buster-captcha-solver-fo/admkpobhocmdideidcndkfaeffadipkc): Captcha Solver for Humans.
  - [floccus](https://microsoftedge.microsoft.com/addons/detail/floccus-bookmarks-sync/gjkddcofhiifldbllobcamllmanombji): bookmarks sync.
  - [TabCloud](https://chromewebstore.google.com/detail/tabcloud/npecfdijgoblfcgagoijgmgejmcpnhof): Save and restore window sessions over time and across multiple Browser.
  - [Bitwarden](https://microsoftedge.microsoft.com/addons/detail/bitwarden-password-manage/jbkfoedolllekgbhcbcoahefnbanhhlh): Password Manager.
  - [Proton Pass](https://chromewebstore.google.com/detail/proton-pass-free-password/ghmbeldphafepmbegfdlkpapadhbakde): FOSS Password Manager, Alternative to `Bitwarden`.
  - [Google Translate](https://chromewebstore.google.com/detail/google-translate/aapbdbdomjkkjkaonfhkkikfgjllcleb): View translations easily as you browse the web.
  - [Absolute Enable Right Click & Copy](https://microsoftedge.microsoft.com/addons/detail/absolute-enable-right-cli/enkbbdhdmbpfohfkfmdmjkpmolkbelgl): Force Enable Right Click & Copy.
  - [UltraWideo](https://chromewebstore.google.com/detail/ultrawideo/bfbnagnphiehemkdgmmficmjfddgfhpl): that manipulates video aspect ratio to fit your entire screen.
  - [Search by Image](https://microsoftedge.microsoft.com/addons/detail/search-by-image/hckehkfhdkpmdlonmjaagiodlpjbonmc): A powerful reverse image search tool, with support for various search engines, such as Google, Bing, Yandex, Baidu and TinEye.
  - [Redirect AMP to HTML](https://microsoftedge.microsoft.com/addons/detail/redirect-amp-to-html/abjhjmfkmdfggjomfpojjfcehhkambcc): Automatically redirects AMP pages to their canonical HTML equivalent.
  - [AI Grammar Checker & Paraphraser](https://microsoftedge.microsoft.com/addons/detail/ai-grammar-checker-para/hfjadhjooeceemgojogkhlppanjkbobc): Instantly Enhance Your Texts with this.
  - [BlockSite](https://microsoftedge.microsoft.com/addons/detail/blocksite-block-websites/lbnblmjlpifpfpefbcgefbhnlcnnjgjk): Block Websites.
  - [ChatGPT for Google](https://chromewebstore.google.com/detail/chatgpt-for-google/jgjaeacdkonaoafenlfkkkmbaopkbilf): Display ChatGPT response alongside search engine results.
  - [ClearURLs](https://microsoftedge.microsoft.com/addons/detail/clearurls/mdkdmaickkfdekbjdoojfalpbkgaddei): Remove tracking elements from URLs.
  - [Cookie AutoDelete](https://microsoftedge.microsoft.com/addons/detail/cookie-autodelete/djkjpnciiommncecmdefpdllknjdmmmo): Automatically delete unwanted cookies from your closed tabs while keeping the ones you want.
  - [Dark Reader](https://microsoftedge.microsoft.com/addons/detail/dark-reader/ifoakfbpdcdoeenechcleahebpibofpc): Dark mode for every website.
  - [Don't F*** With Paste](https://chromewebstore.google.com/detail/dont-f-with-paste/nkgllhigpcljnhoakjkgaieabnkmgdkb): Prevents the blocking of copying from & pasting into input fields.
  - [Enhancer for YouTube™](https://microsoftedge.microsoft.com/addons/detail/enhancer-for-youtube%E2%84%A2/dlgfaleeejmphhnemjgiaekdbonkagkd): Take control of YouTube and boost your user experience!
  - [Firefox Relay](https://chromewebstore.google.com/detail/firefox-relay/lknpoadjjkjcmjhbjpcljdednccbldeb): Firefox Relay makes it easy to create email masks that forward to your true inbox.
  - [Google Analytics Opt-out Add-on (by Google)](https://chromewebstore.google.com/detail/google-analytics-opt-out/fllaojicojecljbmefodhfapmkghcbnh): Tells the Google Analytics JavaScript not to send information to Google Analytics.
  - [Google Keep Chrome Extension](https://chromewebstore.google.com/detail/google-keep-chrome-extens/lpcaedmchfhocbbapmcbpinfpgnhiddi): Save to Google Keep in a single click!
  - [Keepa](https://microsoftedge.microsoft.com/addons/detail/keepa-amazon-price-trac/ejefaeioamebhekmfaclajddbpnnobje): Amazon Price Tracker.
  - [Offline QR Code Generator](https://chromewebstore.google.com/detail/offline-qr-code-generator/fehmldbcmhbdkofkiaedfejkalnidchm): Generate QR codes for the current tab URL.
  - [Honey](https://microsoftedge.microsoft.com/addons/detail/paypal-honey-automatic-c/amnbcmdbanbkjhnfoeceemmmdiepnbpp): Automatic Coupons Find.
  - [Picture-in-Picture Extension (by Google)](https://chromewebstore.google.com/detail/picture-in-picture-extens/hkgfoiooedgoejojocmhlaklaeopbecg): Watch video using Picture-in-Picture.
  - [Privacy Test](https://microsoftedge.microsoft.com/addons/detail/privacy-test/jecjpgpgafmabefacgcfggpofndpbdod): Checks whether you have enhanced private data protection and prevents tracking of your on-line activity.
  - [~~Read Aloud~~](https://microsoftedge.microsoft.com/addons/detail/read-aloud-a-text-to-spe/pnfonnnmfjnpfgagnklfaccicnnjcdkm): A Text to Speech Voice Reader.
  - [Return YouTube Dislike](https://microsoftedge.microsoft.com/addons/detail/return-youtube-dislike/igmhaaclmpaphpnhglgkofddjeafncbj): Returns ability to see dislikes.
  - [Save to Google Drive](https://chromewebstore.google.com/detail/save-to-google-drive/gmbmikajjgmnabiglmofipeabaddhgne): Save web content or screen capture directly to Google Drive.
  - [Scroll To Top](https://chromewebstore.google.com/detail/scroll-to-top/hegiignepmecppikdlbohnnbfjdoaghj): Scroll to top and vice versa in a window.
  - [Seedr](https://chromewebstore.google.com/detail/seedr/abfimpkhacgimamjbiegeoponlepcbob): Download and play Torrent Seeding.
  - [SponsorBlock for YouTube](https://microsoftedge.microsoft.com/addons/detail/sponsorblock-for-youtube-/mbmgnelfcpoecdepckhlhegpcehmpmji): Skip Sponsorships.
  - [Tampermonkey](https://microsoftedge.microsoft.com/addons/detail/tampermonkey/iikmkjmpaadaobahmlepeloendndfphd): userscripts manager.
  - [Temp Mail](https://chromewebstore.google.com/detail/temp-mail-disposable-temp/inojafojbhdpnehkhhfjalgjjobnhomj): Disposable Temporary Email.
  - [Thumbnail Rating Bar for YouTube™](https://microsoftedge.microsoft.com/addons/detail/thumbnail-rating-bar-for-/mglepphnjnfcljjafdgafoipiakakbin): Displays a rating bar (likes/dislikes) on the bottom of every YouTube™ video thumbnail.
  - [uBlacklist](https://chromewebstore.google.com/detail/ublacklist/pncfbmialoiaghdehhbnbhkkgmjanfhe): Blocks sites you specify from appearing in Google search results.
  - [Unhook](https://microsoftedge.microsoft.com/addons/detail/unhook-remove-youtube-r/hebpjnnclppdnfghdnmhgdljmjpfhggk): Remove YouTube Recommended.
  - [Url Shortener](https://microsoftedge.microsoft.com/addons/detail/url-shortener/ajedojkedficaboemnhahoclgfnooelm): The best way to create short links using TinyUrl.
  - [Video Resumer](https://chromewebstore.google.com/detail/video-resumer/bongjkoajofkfpofginnhecihgaeldpe): Automatically resumes YouTube videos from where you played them last.
  - [Video Roll](https://microsoftedge.microsoft.com/addons/detail/video-roll-allinone-v/indeeigndpaahbcegcanpmbenmkbkmmn): Rotate watching video.
  - [WA Web Plus by Elbruz Technologies](https://chromewebstore.google.com/detail/wa-web-plus-by-elbruz-tec/ekcgkejcjdcmonfpmnljobemcbpnkamh): Add more tools and options for WhatsApp Web for more privacy and reliability.
  - [WOT](https://microsoftedge.microsoft.com/addons/detail/wot-website-security-s/iiclaphjclecagpkkaacljnpcppnoibi): Website Security & Safety Checker.
  </details>

- [Opera](https://www.opera.com/browsers/opera): Faster, safer and smarter than default browsers, most stable chromium browser, better than [Chrome](https://play.google.com/store/apps/details?id=com.android.chrome).
- [AdGuard for Safari](https://apps.apple.com/us/app/adguard-for-safari/id1440147259?mt=12): ad blocker extension clears all ads in Safari.
- [uBlock Origin Lite](https://apps.apple.com/in/app/ublock-origin-lite/id6745342698): An efficient content blocker for Safari.
- [Nightshift Dark Mode](https://github.com/unmade/Nightshift): Dark mode for Safari.
- [Userscripts](https://github.com/quoid/userscripts): User Script and Style Manager for Safari.
- [PiPifier](https://apps.apple.com/us/app/pipifier/id1160374471?mt=12): Safari extension that lets you use every HTML5 video in Picture in Picture mode.
- [Bitwarden](https://github.com/bitwarden/clients/releases): open source cross platform password manager.
- [Proton Pass](https://proton.me/pass): FOSS Password Manager

Cloud Drive

- [Google Drive](https://dl.google.com/drive-file-stream/GoogleDrive.dmg): Google cloud storage.

Communication

- [Telegram](https://apps.apple.com/us/app/telegram/id747648890?mt=12): cloud-based cross platfrom messaging app with a focus on security and speed
- [materialgram](https://github.com/kukuruzka165/materialgram/actions/workflows/mac_packaged.yml): [Telegram Desktop](https://github.com/telegramdesktop/tdesktop) fork with Material Design UI
- [WhatsApp](https://apps.apple.com/us/app/whatsapp-messenger/id310633997): instant messaging service provide by Meta
- [Session Desktop](https://github.com/oxen-io/session-desktop/releases): open source cross platform Onion routing based messenger
- [Thunderbird](https://www.thunderbird.net/en-US/download/): free and open-source email client.
- [Betterbird](https://www.betterbird.eu/downloads/): A fork of Mozilla Thunderbird
  <details><summary>
  Top 5 Thunderbird Extensions
  </summary>
      
  - [uBlock Origin](https://addons.thunderbird.net/en-US/thunderbird/addon/ublock-origin/): Ads & Tracker Blocker
  - [Dark Reader](https://addons.thunderbird.net/en-us/thunderbird/addon/darkreader/): Dark mode for every email.
  - [Web Translate](https://addons.thunderbird.net/en-US/thunderbird/addon/web_translate/): Translator for Thunderbird.
  - [Grammar and Spell Checker](https://addons.thunderbird.net/en-US/thunderbird/addon/grammar-and-spell-checker/): Check your emails for spelling and grammar issues.
  - [New Dark Bird](https://addons.thunderbird.net/En-US/thunderbird/addon/new-dark-bird/): New Dark Bird THEMES.
  - or[Thunderbird Suave](https://addons.thunderbird.net/EN-us/thunderbird/addon/thunderbird-suave/): Thunderbird Suave THEMES.
  </details>
- [ProtonMail](https://proton.me/mail/download): Proton Mail
- [Microsoft Outlook](https://apps.apple.com/in/app/microsoft-outlook/id985367838): Microsoft Outlook

Developer Tools

- [Git](https://formulae.brew.sh/formula/git#default): Distributed revision control system
- [GitHub Desktop](https://github.com/desktop/desktop/releases/latest) - Simple collaboration from your desktop. [GitHub Desktop for Linux](https://github.com/shiftkey/desktop/releases)/[GitHub Mobile for Android](https://play.google.com/store/apps/details?id=com.github.android)/[GitHub Mobile for iOS](https://apps.apple.com/us/app/github/id1477376905)
- [XCode](https://apps.apple.com/us/app/xcode/id497799835?mt=12): create great applications for Mac, iPhone, iPad, Apple TV, Apple Watch and Apple Vision Pro.
- [Command Line Tools for Xcode](https://developer.apple.com/download/all/):
  ```
  xcode-select --install
  ```
- [XcodesApp](https://github.com/XcodesOrg/XcodesApp/releases): The easiest way to install and switch between multiple versions of Xcode
- [iSimulator](https://github.com/wigl/iSimulator/releases): a GUI utility to control the Simulator, and manage the app installed on the simulator.
- [Android Studio](https://developer.android.com/studio): official Integrated Development Environment (IDE) for Android app development.
- [android-platfrom-tool](https://formulae.brew.sh/cask/android-platform-tools#default): Google tool that allows you to use ADB commands for Android devices.
- [JDK](https://formulae.brew.sh/formula/openjdk#default): Java Development Kit
- [apktool](https://formulae.brew.sh/formula/apktool#default): Tool for reverse engineering 3rd party, closed, binary Android apps
- [jd-gui](https://github.com/java-decompiler/jd-gui/releases): A standalone Java Decompiler GUI.
- [cutter](https://github.com/rizinorg/cutter): FOSS Reverse Engineering Platform
- [PowerShell](https://github.com/PowerShell/PowerShell): Microsoft PowerShell

Downloader

- [Homebrew](https://brew.sh/): Another Package Manager for macOS.
  - [Xcode Releases](https://developer.apple.com/support/xcode/) + [Additional tools](https://developer.apple.com/download/all/?q=16.2)
  - install Homebrew on macOS:
    ```
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
  - Common cask commands:
    - Update the Homebrew:
      ```
      brew update
      ```
    - Search for available apps:
      ```
      brew search --cask <app_name>
      ```
    - Installs the specified app:
      ```
      brew install --cask <app_name>
      ```
    - Lists all outdated apps:
      ```
      brew outdated
      ```
    - Upgrades the specified app to the latest version:
      ```
      brew upgrade --cask <app_name>
      ```
    - Upgrades the all outdated apps:
      ```
      brew upgrade
      ```
    - Lists all installed binary:
      ```
      brew list --formulae
      ```
    - Lists all installed apps:
      ```
      brew list --cask
      ```
    - Uninstalls the specified app:
      ```
      brew uninstall --cask <app_name>
      ```
  - Example:
    To install the Visual Studio Code app using Homebrew cask, you would run:
    ```
    brew install --cask visual-studio-code
    ```
  - Completely uninstall the Homebrew package manager from macOS:
    ```
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"
    ```
- [App Downloader](https://github.com/yep/app-downloader/releases) - Easily search and download macOS apps from the homebrew
- [Cakebrew](https://github.com/brunophilipe/Cakebrew/releases): Manage your Homebrew
- [yt-dlp](https://github.com/arghya339/ytdl): command-line audio/video downloader
- [MacYTDL](https://github.com/section83/MacYTDL/releases): GUI front-end video/audio downloader based on yt-dlp

Education

- [gcc](https://formulae.brew.sh/formula/gcc#default): C++ Compiler + [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools) + [C/C++ Extension Pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools-extension-pack)
- [easyeda](https://formulae.brew.sh/cask/easyeda#default): PCB design tool
- [kicad](https://formulae.brew.sh/cask/kicad): Electronics design automation suite

Emulator

- [qemu](https://formulae.brew.sh/formula/qemu): Generic machine emulator and virtualizer.
  - check the qemu binary version:
    ```
    /usr/local/Cellar/qemu/9.2.2/bin/qemu-system-x86_64 --version
    ```
  - create a symlink to qemu-system-x86_64 binary:
    ```
    sudo ln -s /usr/local/Cellar/qemu/9.2.2/bin/qemu-system-x86_64 /usr/local/bin/qemu
    ```
  - or,
    ```
    qemu_version=$(qemu-system-x86_64 --version | grep "QEMU emulator version" | awk '{print $4}') && sudo ln -s /usr/local/Cellar/qemu/$qemu_version/bin/qemu-system-x86_64 /usr/local/bin/qemu && qemu --version
    ```
  - after create a symbolic link so you can use qemu as a command:
    ```
    qemu --version
    ```
  - Run the iso with qemu:
    ```
    qemu-system-x86_64 -cdrom /path/to/your.iso -boot d -m 2G
    ```
    - `qemu-system-x86_64`: qemu binary for x86_64 arch; `-cdrom`: Specifies the path to your iso file; `-boot d`: Tells qemu to boot from the cdrom (the iso file); `-m 2G`: Allocates 2GB of RAM to the virtual machine. You can adjust this based on your system's available memory.
- [UTM](https://GitHub.com/utmapp/UTM): full featured system emulator and virtual machine host for iOS and macOS, run Windows, Linux on your Mac.
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads): Powerful open source virtualization for runing Windows, Linux on your Mac.

  iso:
     
     [Windows](https://www.microsoft.com/en-in/software-download)
       
     [Debian](https://www.debian.org/) → [Ubuntu](https://ubuntu.com/download/desktop) → [Linux Mint](https://linuxmint.com/download.php) // [Zorin OS](https://zorin.com/os/download/)

  └── [Kali Linux](https://www.kali.org/get-kali/#kali-platforms)

     [Arch Linux](https://archlinux.org/download/) → [Manjaro](https://manjaro.org/products/download/x86)

     [Fedora](https://fedoraproject.org/workstation/download)

     [openSUSE](https://get.opensuse.org/desktop/)
- ~~[BlueStacks](https://www.bluestacks.com/download.html): World's #1 Android Emulator.~~ Only support on arm based M1/M2/M3/M4 mac.
- [Genymotion](https://www.genymotion.com/product-desktop/download/): Android Emulator on both arm, x86 mac. + [Genymotion Account Register](https://www-v1.genymotion.com/account/create/).
- [Dolphin Emulator](https://dolphin-emu.org/download/): emulator for two recent Nintendo video game(GameCube and Wii) consoles
- [OpenEmu](https://github.com/OpenEmu/OpenEmu/releases): Retro video game emulation for macOS
- [MiniSim](https://github.com/okwasniewski/MiniSim/releases) - MacOS menu bar app for launching iOS and Android emulators.

Entertainment

- [FreeTube](https://github.com/FreeTubeApp/FreeTube/releases): feature-rich and user-friendly YouTube client with a focus on privacy.

Finance

- [crypto-bar](https://github.com/geraldoramos/crypto-bar/releases): A menu bar app that updates cryptocurrencies prices in real-time

Games

- [Steam](https://store.steampowered.com/about/): the ultimate destination for playing and discussing games.
- [PUBG](https://store.steampowered.com/app/578080/PUBG_BATTLEGROUNDS/): Play PUBG BATTLEGROUNDS for free.

Graphics & Design

- [Blender](https://www.blender.org/download/) - Blender is the free and open source 3D creation suite. It supports the entirety of the 3D pipeline: modeling, rigging, animation, simulation, rendering, compositing, motion tracking, and video editing.
- [Krita](https://krita.org/en/download/) - Krita is a cross-platform application for creating digital art files from scratch like illustrations, concept art, matte painting, textures, comics and animations.
- [Pencil2D Animation](https://github.com/pencil2d/pencil/releases) - Pencil2D is an animation/drawing software for macOS, Windows, and Linux. It lets you create traditional hand-drawn animation (cartoon) using both bitmap and vector graphics.
- [inkscape](https://inkscape.org/): free vector design tool
- [godot](https://github.com/godotengine/godot/releases): Multi-platform 2D and 3D game engine
- [Affinity Publisher](https://affinity.serif.com/en-gb/publisher/): next generation of professional page layout software.
- [OpenToonz](https://github.com/opentoonz/opentoonz/releases): Open-source 2D Animation Production Software

IDE

- [VS Code](https://code.visualstudio.com/): powerfull ide + [Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner)
  - [cline](https://github.com/cline/cline): Autonomous coding agent right in your IDE.
  - [continue](https://github.com/continuedev/continue): Create, share, and use custom AI code assistants with this open-source IDE extensions.
- [vscodium](https://github.com/VSCodium/vscodium/releases): VS Code without MS branding/telemetry/licensing
- [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download/?section=mac): The IDE for Java and Kotlin enthusiasts.
- [macdown](https://github.com/MacDownApp/macdown/releases): Open source Markdown editor for macOS.
- [MarkText](https://github.com/marktext/marktext/releases): A simple and elegant cross-platfrom markdown editor

Lifestyle

- [Sinric.Pro web](https://portal.sinric.pro/dashboard): simple way to connect your smart device to Google Home & it's free open source

Music

- [YouTube Music](https://github.com/th-ch/youtube-music/releases/latest): YouTube Music Desktop App bundled with custom plugins (and built-in ad blocker / downloader)
- [spotube](https://github.com/KRTirtho/spotube/releases): Open source Spotify client
- [aural](https://github.com/kartik-venugopal/aural-player): audio player
- [museeks](https://github.com/martpie/museeks/releases): A simple, clean and cross-platform music player
- [BoringNotch](https://github.com/TheBoredTeam/boring.notch): dynamic music control center 

Navigation

- [GPSD](https://formulae.brew.sh/formula/gpsd#default): Global Positioning System (GPS) daemon

- [QGIS](https://qgis.org/download/): open source, cross platform geographical information system (GIS)

News

- [NetNewsWire](https://github.com/Ranchero-Software/NetNewsWire/releases): RSS reader for macOS + https://9to5mac.com/feed/

Notes

- [notesnook](https://github.com/streetwriters/notesnook/releases): open source & cross platform end-to-end encrypted note taking alternative to Evernote.
- [keep](https://github.com/andrepolischuk/keep/releases): Desktop app for Google Keep Notes packaged with Electron
- [Standard Notes](https://github.com/standardnotes/app/releases/latest) : end-to-end encryption sync cross platform notes taking apps

Personalisation

- [Karabiner-Elements](https://github.com/pqrs-org/Karabiner-Elements/releases): powerful key remapper for macOS.
- [OpenRGB](https://gitlab.com/CalcProgrammer1/OpenRGB/-/releases/): Open source RGB lighting control software.
- [Shifty](https://github.com/thompsonate/Shifty/releases): Scheduled Dark Mode
- [MonitorControl](https://github.com/MonitorControl/MonitorControl/releases): show brighitness/volume slider in mac menu using monitor Display Data Channel/Command Interface(DDC/CI) controller over VGA/HDMI/DP/Type-C.
- [Lunar](https://github.com/alin23/Lunar/releases) - Intelligent adaptive brightness for your external displays.
- [KeepingYouAwake](https://github.com/newmarcel/KeepingYouAwake/releases): Prevents your Mac from going to sleep.
- [Mos](https://github.com/Caldis/Mos/releases): Reverse the mouse wheel scroll direction
- [Rectangle](https://github.com/rxhanson/Rectangle/releases): Move and resize windows on macOS

Photo & Video

- [DavinchiResolve](https://apps.apple.com/in/app/davinci-resolve/id571213070?mt=12): Professional video editing tools, Alternative to Apple Logic Pro
- [iMovie](https://apps.apple.com/in/app/imovie/id408981434?mt=12): create beautiful movies that you can edit at resolutions up to 4K.
- [Jitsi Meet Electron](https://github.com/jitsi/jitsi-meet-electron/releases): Jitsi Meet desktop application powered by React native
- [Ente Photos](https://github.com/ente-io/photos-desktop): open source cross platform end-to-end encryption sync Photos app Alternative to Google Photos & Apple Photos.
- [GIMP](https://www.gimp.org/downloads/): Free & Open Source Image Editor
- [darktable](https://github.com/darktable-org/darktable/releases): free Adobe Lightroom Classic replacement.

Player

- [VLC](https://www.videolan.org/vlc/download-macosx.html): free and open source cross-platform multimedia player
- [iina](https://github.com/iina/iina/releases): The modern video player for macOS Based on mpv, alternative to vlc.

Productivity

- [Microsoft To Do](https://apps.apple.com/in/app/microsoft-to-do/id1274495053): Capture Tasks & Set Reminders.
- [Microsoft Office](https://formulae.brew.sh/cask/microsoft-office): OneDrive, Microsoft Excel, Microsoft Word, Microsoft OneNote, Microsoft PowerPoint, Microsoft Outlook, Defender. + [Microsoft-Office-For-MacOS](https://github.com/alsyundawy/Microsoft-Office-For-MacOS/releases): Activited Microsoft Office For MacOS.
- [Keynote](https://apps.apple.com/us/app/keynote/id409183694?mt=12): free powerful presentations app by Apple
- [Pages](https://apps.apple.com/us/app/pages/id409201541?mt=12): Create gorgeous documents in minutes
- [Numbers](https://apps.apple.com/us/app/numbers/id409203825?mt=12): Create gorgeous spreadsheets
- [LibreOffice](https://www.libreoffice.org/download/download-libreoffice/?type=mac-x86_64): free and powerful office suite, Alternative to Microsoft Office
- [Google-Assistant-Unofficial-Desktop-Client](https://github.com/Melvin-Abraham/Google-Assistant-Unofficial-Desktop-Client/releases): cross-platform unofficial Google Assistant Client for Desktop
- [MacAssistant](https://github.com/vanshg/MacAssistant/releases): Google Assistant for macOS menu bar!
- [inshellisense](https://github.com/microsoft/inshellisense): IDE style command line auto complete, Requirements [Node.js](https://formulae.brew.sh/formula/node)
- [ohmyzsh](https://github.com/ohmyzsh/ohmyzsh?tab=readme-ov-file#basic-installation): managing Themes your zsh configuration.
  > uninstall ohmyzsh: `bash ~/.oh-my-zsh/tools/uninstall.sh`
- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions): Fish-like autosuggestions for zsh.
  <details><summary>
  zsh-autosuggestions installation
  </summary>
  
  - Clone zsh-autosuggestions repo:
  ```
  git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
  ```
  - Add zsh-autosuggestions source:
  ```
  echo "source ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
  ```
  - Restart macOS Terminal: Close and Reopen
  - Done.
  </details>
- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting): Fish shell like syntax highlighting for Zsh.
  <details><summary>
  zsh-syntax-highlighting installation
  </summary>
  
  - Clone zsh-syntax-highlighting repo:
  ```
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
  ```
  - Add zsh-syntax-highlighting source:
  ```
  echo "source ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
  ```
  - Restart macOS Terminal: Close and Reopen
  - Done.
  </details>
 <details><summary>
 Customize macOS Terminal
 </summary>

 - Uncheck `Resotre text when reopening windows` option in Terminal > Settings > Profiles > Window
 - Open Terminal > from macOS menubar go Terminal > Settings... > Profiles > Text > Cursor > Select `Vertical Bar` & `Blink cursor`
 - Open Terminal > from macOS menubar go Terminal > Settings... > Profiles > Text > Background > Color & Effects > `Opacity`: `75%` & `Blur`: `45%`
 - Open Terminal > from macOS menubar go Terminal > Settings... > Profiles > Text > Background > Image: > `Choose...` > Downloads > [kali-neon.png](https://www.kali.org/wallpapers/images/2020.4/kali-neon.png) > Open.
 - Restart macOS Terminal: Close and Reopen
 </details>

- [Powerlevel10k](https://github.com/romkatv/powerlevel10k): zsh Theme
- [prezto](https://github.com/sorin-ionescu/prezto): zsh configuration for auto completion, and prompt themes.

Screensaver

- [Aerial](https://github.com/JohnCoates/Aerial/releases) - Apple TV Aerial Screensaver for macOS. 

Security

- [VirusTotal](https://docs.virustotal.com/docs/desktop-apps#mac-os-x-uploader): Drag and drop files scan
- [Avast antivirus](https://www.avast.com/en-in/free-mac-security#mac): best free antivirus for Mac
- [Cryptomator](https://cryptomator.org/downloads/): Multi-platform transparent client-side encryption of your files in the cloud
- [LuLu](https://github.com/objective-see/LuLu/releases): macOS firewall
- [BLEUnlock](https://github.com/ts1/BLEUnlock): Lock/unlock your Mac with your any Bluetooth LE devices
- [EnteAuth](https://github.com/ente-io/ente/releases?q=auth&expanded=true): Open Source Authenticator with cross platform end-to-end encryption data sync.

  <details><summary>
  Correct Timezone
  </summary>

  - macOS Timezone files are located in `/usr/share/zoneinfo` dir
  - you can see available zoneinfo in mac using this command:
    ```
    sudo ls /usr/share/zoneinfo
    ```
    or,
    ```
    cd /usr/share/zoneinfo && zoneinfo ls
    ```
  > Now you can see the seven continents of the world are `Asia`, `Africa`, `North America`, `South America`, `Antarctica`, `Europe`, and 
  `Australia`.
  
  > for my case me from `Asia` continent and you can see a row in this continent this continent row has list of countries name: `EET` `GB` `Eire` 
  `Indian` `MST7MDT` `Portugal` `W-SU`
  
  > for my case me `Indian`
  
  > and my countries has more then one City and my city is `Calcutta`

  - or, you can use this command to view list of available zoneinfo in mac:
    ```
    sudo systemsetup -listtimezones
    ```

  > so my zone is `Asia/Calcutta`

  - so i can use this command to set `Asia/Calcutta` as my Timezone:
    ```
    sudo systemsetup -settimezone Asia/Calcutta
    ```

  > Now you can visit [time.is](https://time.is/) website to verify Your time is exact! or not (behind/ ahead)!
  </details>

Sharing Files

- [LocalSend](https://apps.apple.com/us/app/localsend/id1661733229): free, open-source, cross-platform file sharing tool that allows you to share files to nearby devices. Alternative to AirDrop.
- [OpenMTP](https://github.com/ganeshrvel/openmtp/releases) - Advanced Android File Transfer Application for macOS (Drag & drop File sharing is working from mac to Android only).
- [NearDrop](https://github.com/grishka/NearDrop/releases): An unofficial Google Nearby Share/Quick Share app for macOS

Social Networking

- [Vencord](https://github.com/Vencord/Installer/releases): Discord Desktop client mod
- [BetterDiscord](https://github.com/BetterDiscord/Installer/releases): enhances Discord desktop app with new features.
- [RedditOS](https://github.com/Dimillian/RedditOS/releases): A SwiftUI Reddit client for macOS

Streaming

- [OBS Studio](https://obsproject.com/download): free and open source software for video recording and live streaming. + [DroidCam OBS Plugins](https://droidcam.app/obs/#): connect your phone and get high quality audio & video directly into OBS Studio, just like a regular camera
- [IriunWebcam](https://iriun.com/) : use your Android phone as a wireless webcam
- [scrcpy](https://github.com/Genymobile/scrcpy/releases): Display and control your Android device
- [QtScrcpy](https://github.com/barry-ran/QtScrcpy/releases): Displaying and controlling Android devices via USB or over Local network.
- [airsync-mac](https://github.com/sameerasw/airsync-mac): adb & media-control to Android + [airsync-android](https://github.com/sameerasw/airsync-android): Android app for AirSync
- [Android tool for Mac](https://github.com/mortenjust/androidtool-mac) - One-click screenshots, video recordings, app installation for iOS and Android
- [Duet Display](https://apps.apple.com/us/app/duet-display/id935754064): turns your Android, iPad or iPhone into the most advanced extra display for your Mac & PC.
- [ChromeRemoteDesktop](https://remotedesktop.google.com/access): control your mac from another device (phone/computer)

System

- [HoRNDIS](https://github.com/jwise/HoRNDIS/releases): Android USB tethering driver for MacOS
- [Heliport](https://github.com/OpenIntelWireless/HeliPort/releases): Intel WiFi Client for itlwm.
- [Hackintool](https://github.com/benbaker76/Hackintool/releases): view system info & generate a `USBPorts.kext` & `SSDT-UIAC.aml`
- [OCSysInfo](https://github.com/KernelWanderers/OCSysInfo/releases): Basic, high-level and efficient CLI for discovering, outputting and parsing hardware information from the current system.
- [fastfetch](https://github.com/fastfetch-cli/fastfetch): [neofetch](https://github.com/dylanaraps/neofetch) like system information tool.
- [kextupdater](https://github.com/MacThings/kextupdater/releases): update kext, OC/EFI
- [EFI-Agent](https://github.com/benbaker76/EFI-Agent/releases): GUI based tool to Mount Hidden EFI partitions, Alternative to MountEFI.cmd
- [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools/releases): GUI based tool to Mount hidden system EFI & update kext, OpenCore/EFI driver & save changes to config.plist
- [MaciASL](https://github.com/acidanthera/MaciASL/releases): ACPI editing IDE for macOS.
- [VDADecoderChecker](https://i.applelife.ru/2019/05/451893_10.12_VDADecoderChecker.zip): check dGPUs DRM (Hardware Acceleration and Decoding) support is working.

Tools

- [Stats](https://github.com/exelban/stats/releases): macOS system monitor (CPU utilization, GPU utilization, Memory usage, Disk utilization, Network usage, Fan's control) in your menu bar.
- [BarTranslate](https://github.com/ThijmenDam/BarTranslate) - A handy menu bar translator app that supports DeepL and Google Translate.
- [pot-desktop](https://github.com/pot-app/pot-desktop/releases): cross-platform software for text translation and recognition.

Utilities

- [Balena Etcher](https://github.com/balena-io/etcher) - Flash OS images to SD cards & USB drives, safely and easily.
- [Keka](https://github.com/aonez/Keka/releases): The macOS & iOS file archiver (zip,rar,7z)
- [HandBrake](https://github.com/HandBrake/HandBrake/releases) : video transcoder (mkv/mp4)
- [Czkawka](https://github.com/qarmin/czkawka/releases): remove unnecessary (Temporary, Duplicates etc.) files from your computer.

VPN & Proxy

- [DNS Changer](https://github.com/DnsChanger/dnsChanger-desktop/releases): DNS Changer
- [Gas Mask](https://github.com/2ndalpha/gasmask/releases): hosts file manager + [StevenBlack/hosts](https://github.com/StevenBlack/hosts/blob/master/hosts): StevenBlack Unified hosts = (adware + malware)
- [Cloudflare WARP](https://1.1.1.1/): makes your Internet more private 
- [WireGuard](https://WireGuard.com/install/): WireGuard is a fast, modern, and secure VPN tunnel. + [WireGuard Config by ProtonVPN](https://account.protonvpn.com/downloads#wireguard-configuration): The best VPN for speed and security.
- [OpenVPN](https://openvpn.net/client/#tab-macos): FOSS VPN daemon, Alternative to [WireGuard](https://github.com/WireGuard/wireguard-apple). + [OpenVPN Config by ProtonVPN](https://account.protonvpn.com/downloads#openvpn-configuration-files) + [OpenVPN Connect for macOS](https://openvpn.net/client-connect-vpn-for-mac-os/) + [OpenVPN / IKEv2 username](https://account.protonvpn.com/account-password#openvpn)
- [Tunnelblick](https://github.com/Tunnelblick/Tunnelblick/releases): FOSS OpenVPN GUI. + [OpenVPN Config by ProtonVPN](https://account.protonvpn.com/downloads#openvpn-configuration-files) +  [OpenVPN on macOS using Tunnelblick](https://protonvpn.com/support/mac-vpn-setup) + [OpenVPN / IKEv2 username](https://account.protonvpn.com/account-password#openvpn)
- [AdGuard VPN](https://adguard-vpn.com/en/mac/overview.html): AdGuard VPN for macOS
- [Orbot](https://apps.apple.com/us/app/orbot/id1609461599): Open-source Tor-powered VPN.

Wallpaper

- [BingWallpaper](https://github.com/arghya339/BingWallpaper): Change your wallpaper with Bing image of the day.
- [BingPaper](https://github.com/pengsrc/BingPaper/releases) - Use Bing daily photo as your wallpaper on macOS.

Weather

- [DatWeatherDoe](https://github.com/inderdhir/DatWeatherDoe/releases): macOS menu bar weather app

</details>

<details><summary>
    
## 🛒Alder / Raptor Lake Hack Buyer Guide
</summary>

<details><summary>
    
### Motherboard 
</summary>

<details><summary>

#### Motherboard Under $549
</summary>

Motherboard|Chipset|MemoryType|WiFi|LAN|Audio|NotWorking|Price
:----|:----|:----|:----|:----|:----|:----|:----
~~MSI MEG Z790 GODLIKE DDR5~~|Z790|DDR5|Intel AX211|Realtek RTL8125BG 2.5GbE/ Aquantia AQC113C 10GbE|Realtek ALC4082|Audio|$549
~~ASUS ROG Maximus Z790 Hero WiFi~~|Z790|DDR5|Intel AX210|Intel I225-V 2.5GbE|ROG SupremeFX ALC4082|Audio|$506
~~MSI MPG Z790 EDGE WiFi DDR4~~|Z790|DDR4|Intel AX211|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$468
~~ASUS ROG Strix Z790-I Gaming WiFi~~|Z790|DDR5|Intel AX211|Intel I226-V 2.5GbE|Realtek ALC4050|Audio|$433
ASUS ProArt Z790 Creator WiFi|Z790|DDR5|Intel AX211|Intel I225/I226-V 2.5GbE/ Marvell AQtion AQC107 10GbE|Realtek S1220A|-|$439
~~MSI MPG Z790 CARBON WiFi DDR5~~|Z790|DDR5|Intel AX211|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$418
</details>

<details><summary>

#### Motherboard Under $379
</summary>

Motherboard|Chipset|MemoryType|WiFi|LAN|Audio|NotWorking|Price
:----|:----|:----|:----|:----|:----|:----|:----
ASUS ROG STRIX B660-I GAMING WiFi|B660|DDR4|Intel AX201|Intel I225-V 2.5GbE|ROG SupremeFX ALC1220A|-|$379
~~ASRock Z790 TAICHI CARRARA DDR5~~|Z790|DDR5|Intel Killer AX1675x|Intel Killer E3100 2.5GbE|Realtek ALC4082|WiFi/ LAN/ Audio|$389
~~ASUS ROG STRIX Z790-F GAMING WiFi~~|Z790|DDR5|Intel AX210|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$386
~~MSI MPG Z790 CARBON WiFi DDR5~~|Z790|DDR5|Intel AX211|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$386
ASUS TUF Gaming Z690-Plus WiFi|Z690|DDR5|Intel AX210|Intel I225-V 2.5GbE|Realtek ALC897|-|$383
~~ASRock Z790 TAICHI DDR5~~|Z790|DDR5|Intel Killer AX1675x|Intel Killer E3100 2.5GbE|Realtek ALC4082|WiFi/ LAN/ Audio|$379
~~ASUS ROG Strix Z790-E Gaming WiFi~~|Z790|DDR5|Intel AX210|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$379
ASUS Prime Z790-P WiFi D4|Z790|DDR4|Intel AX200|Intel I225-V 2.5GbE|Realtek ALC897|-|$339
~~MSI PRO Z790-A WiFi DDR4~~|Z790|DDR4|Intel AX210|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$369
~~ASUS ROG Strix Z790-A Gaming WiFi D4~~|Z790|DDR4|Intel AX210|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$365
ASUS Prime Z690-P WiFi D4|Z690|DDR4|Intel AX200|Intel I225-V 2.5GbE|Realtek ALC897|-|$334
~~MSI MEG Z790 ACE DDR5~~|Z790|DDR5|Intel AX210|Intel I225/I226 2.5GbE|Realtek ALC4082|Audio|$359
~~MSI PRO Z790-A WiFi DDR5~~|Z790|DDR5|Intel AX210|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$354
</details>

<details><summary>

#### Motherboard Under $349
</summary>

Motherboard|Chipset|MemoryType|WiFi|LAN|Audio|NotWorking|Price
:----|:----|:----|:----|:----|:----|:----|:----
~~ASRock Z790 PG-ITX/TB4 DDR5~~|Z790|DDR5|Intel Killer AX1675x|Intel Killer E3100G 2.5GbE|Realtek ALC4082|WiFi/ LAN/ Audio|$349
~~ASUS ROG STRIX B660-A GAMING WiFi D4~~|B660|DDR4|Intel AX200|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$319
MSI MPG B760I EDGE WiFi DDR4|B760|DDR4|Intel AX211|Realtek RTL8125BG 2.5Gbps|Realtek ALC897|-|$318
~~MSI MAG Z790 TOMAHAWK WiFi DDR4~~|Z790|DDR4|Intel AX211|Realtek RTL8125B 2.5GbE|Realtek ALC4080|Audio|$339
GIGABYTE B660I AORUS PRO DDR4|B660|DDR4|Intel AX200/ AX201/ AX211|Intel I225-V 2.5GbE|Realtek ALC897|-|$302
GIGABYTE Z790 AORUS MASTER X |Z790|DDR5|Qualcomm QCNCM865 / AMD RZ738 (MediaTek MT7927) / Intel BE200|Marvell AQtion AQC113 10GbE|Realtek ALC1220-VB|Qualcomm QCNCM865 / AMD RZ738 (MediaTek MT7927) / Intel WiFi@6GHz|$329
~~ASUS ROG STRIX Z690-A GAMING WiFi D4~~|Z690|DDR4|Intel AX200|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$418
GIGABYTE B660M AORUS PRO AX DDR4|B660|DDR4|Intel AX200/ AX211|Intel I225-V 2.5GbE|Realtek ALC897|-|$288
GIGABYTE Z790 UD AX DDR5|Z790|DDR5|Intel AX210|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|$275
~~MSI MPG Z790I EDGE WiFi DDR5~~|Z790|DDR5|Intel AX211|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$302
</details>

<details><summary>

#### Motherboard Under $299
</summary>

Motherboard|Chipset|MemoryType|WiFi|LAN|Audio|NotWorking|Price
:----|:----|:----|:----|:----|:----|:----|:----
ASRock Z690 Phantom Gaming-ITX/TB4|Z690|DDR5|Intel Killer AX1675|Intel Killer E3100 2.5GbE|Realtek ALC1220|WiFi/ LAN|$299
~~MSI MPG Z790 EDGE WiFi DDR5~~|Z790|DDR5|Intel AX211|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$293
GIGABYTE B660M AORUS ELITE AX DDR4|B660|DDR4|Intel AX211|Realtek RTL8125BG 2.5GbE|Realtek ALC897|-|$258
~~MSI MAG B760M MORTAR WiFi~~|B760|DDR5|Intel AX210|Realtek RTL8125BG 2.5GbE|Realtek ALC4080|Audio|$258
ASUS PRIME B660M-A WiFi D4|B660|DDR4|Intel AX200|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|$258
MSI MAG B660M MORTAR WiFi DDR4|B660|DDR4|Intel AX200|Realtek 8125BG 2.5Gbps|Realtek ALC1200|-|$254
ASUS Prime Z790-A WiFi|Z790|DDR5|Intel AX211|Intel I225-V 2.5G|Realtek S1220A|-|$279
~~MSI MPG Z790 EDGE TI MAX WiFi DDR5~~|Z790|DDR5|Intel BE200|Intel I225-V 2.5GbE|Realtek ALC4080|WiFi@6GHz/ Audio|$278
</details>

<details><summary>

#### Motherboard Under $245
</summary>

Motherboard|Chipset|MemoryType|WiFi|LAN|Audio|NotWorking|Price
:----|:----|:----|:----|:----|:----|:----|:----
MSI PRO Z690-A WiFi DDR4|Z690|DDR4|Intel AX201|Intel I225-V 2.5GbE|Realtek ALC897|-|$245
ASUS TUF GAMING B660M-PLUS WiFi D4|B660|DDR4|Intel AX200|Realtek RTL8125BG 2.5GbE|Realtek ALC897|-|$238
GIGABYTE B760 GAMING X AX DDR4|B760|DDR4|Intel AX210|Realtek RTL8125BG|Realtek ALC897|-|$223
MSI Z790 PROJECT ZERO WiFi DDR5|Z790|DDR5|Intel BE200|Intel 2.5Gbps|Realtek ALC897|WiFi@6GHz|$249
GIGABYTE Z790 AORUS PRO X WiFi 7 DDR5|Z790|DDR5|Intel BE200|Realtek RTL8125BG 5GbE|Realtek ALC1220-VB|WiFi@6GHz|$299
~~MSI MAG Z790 TOMAHAWK MAX WiFi DDR5~~|Z790|DDR5|Intel BE200|Intel 2.5Gbps|Realtek ALC4080|Audio|$249
GIGABYTE Z690 AORUS ELITE AX DDR4|Z690|DDR4|Intel AX201|Realtek RTL8125B 2.5GbE|Realtek ALC1220-VB|-|$248
~~GIGABYTE Z790 AORUS ELITE AX DDR4~~|Z790|DDR4|Realtek RTL8852CE / Intel AX211|Realtek RTL8125B 2.5GbE|Realtek ALC4080|Realtek RTL8852CE / Audio|$245
GIGABYTE Z790 AERO G DDR5|Z790|DDR5|Intel AX211|Intel I225-V 2.5GbE|Realtek ALC1220-VB|-|$239
~~ASUS ROG Strix B760-F Gaming WiFi~~|B760|DDR5|Intel AX211|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$239
~~GIGABYTE Z790 AORUS ELITE AX DDR5~~|Z79|DDR5|Intel AX211|Realtek RTL8125B 2.5GbE|Realtek ALC4080|Audio|$219
ASUS TUF Gaming Z790-Plus WiFi|Z790|DDR5|Intel AX211|Intel 2.5GbE|Realtek ALCS1220A|-|$229
ASUS ROG STRIX Z790-H Gaming WiFi|Z790|DDR5|Intel AX211|Intel I225/I226 2.5GbE|Realtek ALC1220|-|$229
ASUS TUF Gaming Z690-PLUS WiFi D4|Z690|DDR4|Intel AX211|Intel I225/I226 2.5GbE|Realtek ALC897|-|$389
~~MSI PRO Z790-A MAX WiFi~~|Z790|DDR5|Intel BE200|Intel I225/I226 2.5GbE|Realtek ALC4080|WiFi@6GHz / Audio|$229
MSI MPG B760M EDGE TI WiFi DDR5|B760|DDR5|Intel AX210|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|$219
~~ASUS Z790-AYW WiFi W~~|Z790|DDR5|Intel AX211|Realtek RTL8125B 2.5GbE|Realtek ALC4080|Audio|$219
~~GIGABYTE Z790 GAMING X AX~~|Z790|DDR5|Realtek RTL8852CE / Intel AX210/AX211|Realtek RTL8125B 2.5GbE|Realtek ALC4080|Realtek RTL8852CE / Audio|$219
MSI MAG B760 TOMAHAWK WIFI DDR4|B760|DDR4|Intel AX210|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|$197
MSI Z790 GAMING PLUS WIFI DDR5|Z790|DDR5|Intel AX211|Intel I225/I226 2.5GbE|Realtek ALC897|-|$209
ASRock Z690M-ITX/AX DDR4|Z690|DDR4|Intel AX200/ AX201/ AX211|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|$179
GIGABYTE B760M DS3H AX DDR4|B760|DDR4|AMD RZ608 (MT7921K) / Realtek RTL8852CE / Intel AX210/AX211|Realtek RTL8118/ 8168/ 8411 2.5GbE|Realtek ALC897|AMD RZ608 (MT7921K) / Realtek RTL8852CE|$208
GIGABYTE B760M AORUS ELITE AX DDR5|B760|DDR5|Intel AX211 / Realtek RTL8852CE|Realtek 2.5GbE|Realtek ALC897|Realtek RTL8852CE|$208
MSI MPG B760I EDGE WIFI DDR5|B760|DDR5|Intel AX211|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|$205
</details>

<details><summary>

#### Motherboard Under $199
</summary>

Motherboard|Chipset|MemoryType|WiFi|LAN|Audio|NotWorking|Price
:----|:----|:----|:----|:----|:----|:----|:----
~~MSI MAG Z790 TOMAHAWK WiFi DDR5~~|Z790|DDR5|Intel AX211|Intel 2.5Gbps|Realtek ALC4080|Audio|$199
GIGABYTE Z790 AORUS ELITE AX ICE|Z790|DDR5|Intel AX211 / Realtek RTL8852CE|Realtek 2.5GbE|Realtek ALC897|Realtek RTL8852CE|$199
GIGABYTE Z790 AORUS ELITE X WIFI|Z790|DDR5|AMD RZ738 (MediaTek MT7927) / Qualcomm QCNCM865 / Intel BE200|Intel I225-V 2.5GbE|Realtek ALC1220-VB|AMD RZ738 (MediaTek MT7927) / Qualcomm QCNCM865 / WiFi@6GHz|$199
GIGABYTE B760M Gaming X AX DDR4|Z790|DDR4|Realtek RTL8852CE / Intel AX211|Realtek RTL8118AS 2.5GbE|Realtek ALC897|Realtek RTL8852CE|$169
MSI B760M Project Zero WiFi DDR5|B760|DDR5|Intel AX211|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|$189
GIGABYTE B760I AORUS PRO DDR4|B760|DDR4|Intel AX211 / Intel Killer AX1650|Intel I225 2.5GbE|Realtek ALC897|Intel Killer AX1650|$189
MSI Pro Z790-P WiFi DDR4|Z790|DDR4|Intel AX211|Intel I225/I226 2.5GbE|Realtek ALC897|-|$189
ASRock Pro Z790 Pro RS WiFi DDR5|Z790|DDR5|Intel AX211|Realtek Dragon RTL8125BG 2.5GbE|Realtek ALC897|Intel LAN|$189
ASUS ROG Strix B760-I Gaming WiFi|B760|DDR5|Intel AX211|Intel I225-V 2.5GbE|Realtek ALCS1220A|-|$189
ASUS Prime Z790-P WiFi|Z790|DDR5|Intel AX210|Realtek 2.5GbE|Realtek ALC897|-|$189
MSI PRO Z790-P WiFi DDR5|Z790|DDR5|Intel AX211|Intel I225-V 2.5GbE|Realtek ALC897|-|$185
MSI MAG B760 Tomahawk WiFi|B760|DDR5|Intel AX211|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|$179
GIGABYTE B760 AORUS ELITE AX DDR5|B760|DDR5|Intel AX210|Realtek 2.5GbE|Realtek ALC897|-|$179
MSI MAG B760M Mortar WiFi|B760|DDR5|Intel AX211|Realtek RTL8125B 2.5G|Realtek ALC897|-|$179
~~ASUS ROG Strix Z690-I Gaming WiFi~~|Z690|DDR5|Intel AX210|Intel I225-V 2.5GbE|Realtek ALC4080|Audio|$179
MSI Z790 Gaming Pro WiFi DDR5|Z790|DDR5|Intel AX211|Realtek RTL8125B 2.5GbE / Realtek RTL8111H 1Gbps|Realtek ALC897|Realtek RTL8111H 1Gbps|$179
ASRock Z790 Lightning WiFi DDR5|Z790|DDR5|Intel Killer AX1675x|Intel Killer E3100 2.5GbE|Realtek ALC897|WiFi / LAN|$179
GIGABYTE B760 Gaming X AX DDR5|B760|DDR5|AMD RZ608 (MT7921K) / Realtek RTL8852CE / Intel AX210/AX210|Realtek 2.5GbE|Realtek ALC897|AMD RZ608 (MT7921K) / Realtek RTL8852CE|$169
GIGABYTE Z790 Eagle AX DDR5|Z790|DDR5|Intel AX211 / Realtek RTL8852CE|Realtek 2.5GbE|Realtek ALC897|Realtek RTL8852CE|$169
MSI Pro Z790-VC WiFi DDR5|Z790|DDR5|Intel BE200|Realtek RTL8125BG 2.5Gbps|Realtek ALC897|WiFi@6GHz|$159
ASRock B760M Steel Legend WiFi DDR5|B760|DDR5|Intel AX211|Realtek RTL8125BG 2.5GbE|Realtek ALC897|-|$159
ASRock Z690 PG Velocita DDR5|Z690|DDR5|Intel Killer 1675|Intel Killer E3100 2.5GbE|Realtek ALC1220|Intel WiFi/ Intel LAN|$159
MSI Pro Z790-S WiFi DDR5|Z790|DDR5|Intel AX211|Realtek RTL8125BG 2.5Gbps|Realtek ALC897|-|$158
</details>

<details><summary>

#### Motherboard Under $149
</summary>

Motherboard|Chipset|MemoryType|WiFi|LAN|Audio|NotWorking|PCIe|NVMe M.2|ATX(motherboard)|EPS(cpu)|Fan|Addressable LED|Form Factor|BIOS Quick Flash|Price
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
MSI Pro B760-P WiFi DDR4|B760|DDR4|Intel AX211|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|||||||||$149
MSI Pro B760M-A WiFi DDR4|B760|DDR4|Intel AX211|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|||||||||$149
ASRock B760M Pro RS/D4 WiFi|B760|DDR4|Intel AX201|Realtek RTL8125B 2.5GbE|Realtek ALC897|-|||||||||$149
GIGABYTE Z790 Gaming Plus AX DDR5|Z790|DDR5|Realtek RTL8851BE|Realtek 2.5GbE|Realtek ALC897|WiFi|||||||||$149
GIGABYTE B760 DS3H AX DDR5|B760|DDR5|Realtek RTL8852CE / Intel AX210/AX211|Realtek 1GbE|Realtek ALC897|Realtek RTL8852CE|||||||||$139
GIGABYTE B760M GAMING PLUS WiFi DDR4|B760|DDR4|Realtek RTL8851BE|Realtek 1GbE|Realtek ALC897|WiFi|||||||||$139
GIGABYTE B760M DS3H AX DDR5|B760|DDR5|AMD RZ608 (MT7921K) / Realtek RTL8852CE / Intel AX210/AX211|Realtek 2.5GbE|Realtek ALC897|AMD RZ608 (MT7921K) / Realtek RTL8852CE|||||||||$139
ASRock B760M PG SONIC WiFi DDR5|B760|4x32GB DDR5@4000MHz|Intel Killer AX1675x|Realtek RTL8125BG 2.5GbE|Realtek ALC897|WiFi|1xPCIe 5.0x16|3xPCIe 4.0x4 M.2 2280|1x24-pin|2x8-pin|1x4-pin cpu_f 1x4-pin cpu_pump 3x4pin sys_fan|3x|mATX|Yes|$129
MSI PRO H610M-G WiFi DDR4|H610|2x32GB DDR4@3200MHz|Realtek RTL8852CE / Intel AX211|Intel I219V 1Gbps|Realtek ALC897|Realtek RTL8852CE / LAN|1xPCIe 4.0x16|1xPCIe 3.0x4 M.2 2280|1x24-pin|1x8-pin|1x4-pin cpu_f 1x4-pin sys_f|NA|mATX|-|$89
</details>

</details>

<details><summary>

### Processor
</summary>

<details><summary>

#### CPU Under $549
</summary>

CPU|iGPU|P-Core|E-Core|Threads|P-Core Turbo Frequency|P-Core Base Frequency|E-Core Turbo Frequency|E-Core Base Frequency|Cache|Power|Stock Cooler|Price
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
Intel Core i9-13900F|NA|8|16|32|5.2GHz|2GHz|4.2GHz|1.5GHz|36MB|219W|Intel Laminar RM1|$549
Intel Core i9-14900KF|NA|8|16|32|5.6GHz|3.2GHz|4.4GHz|2.4GHz|36MB|253W|NA|$534
Intel Core i9-14900F|NA|8|16|32|5.4GHz|2GHz|4.3GHz|1.5GHz|36MB|219W|NA|$509
Intel Core i9-13900KF|NA|8|16|32|5.4GHz|3GHz|4.3GHz|2.2GHz|36MB|253W|NA|$474
Intel Core i7-14700KF|NA|8|12|28|5.5GHz|3.4GHz|4.3GHz|2.5GHz|33MB|253W|NA|$364
Intel Core i7-14700F|NA|8|12|28|5.3GHz|2.1GHz|4.2GHz|1.5GHz|35MB|219W|Intel Laminar RM1|$362
Intel Core i7-13700F|NA|8|8|24|5.1GHz|2.1GHz|4.1GHz|1.5GHz|30MB|219W|NA|$359
Intel Core i9-12900F|NA|8|8|24|5GHz|2.4GHz|3.8GHz|1.8GHz|30MB|202W|NA|$348
Intel Core i7-13700KF|NA|8|8|24|5.3GHz|3.4GHz|4.2GHz|2.5GHz|30MB|153W|NA|$324
</details>

<details><summary>

#### CPU Under $299
</summary>

CPU|iGPU|P-Core|E-Core|Threads|P-Core Turbo Frequency|P-Core Base Frequency|E-Core Turbo Frequency|E-Core Base Frequency|Cache|Power|Stock Cooler|Price
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
Intel Core i9-12900KF|NA|8|8|24|5.1GHz|3.2GHz|3.9GHz|2.4GHz|30MB|241W|NA|$299
Intel Core i5-14600KF|NA|6|8|20|5.3GHz|3.5GHz|4GHz|2.6GHz|24MB|181W|NA|$284
Intel Core i7-12700F|NA|8|4|20|4.8GHz|2.1GHz|3.6GHz|1.6GHz|25MB|180W|Intel Laminar RM1|$248
Intel Core i5-13600KF|NA|6|8|20|5.1GHz|3.5GHz|3.9GHz|2.6GHz|20MB|181W|NA|$299
Intel Core i7-12700KF|NA|8|4|20|4.9GHz|3.6GHz|3.8GHz|2.7GHz|12MB|190W|NA|$209
</details>

<details><summary>

#### CPU Under $199
</summary>

CPU|iGPU|P-Core|E-Core|Threads|P-Core Turbo Frequency|P-Core Base Frequency|E-Core Turbo Frequency|E-Core Base Frequency|Cache|Power|Stock Cooler|Price
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
Intel Core i5-14400F|NA|6|4|16|4.7GHz|2.5GHz|3.5GHz|1.8GHz|20MB|148W|Intel Laminar RM1|$199
Intel Core i5-13400F|NA|6|4|16|4.6GHz|2.5GHz|3.3GHz|1.8GHz|20MB|148W|Intel Laminar RM1|$161
Intel Core i5-12600KF|NA|6|4|16|4.9GHz|3.7GHz|3.6GHz|3.8GHz|20MB|150W|NA|$144
Intel Core i3-14100F|NA|4|NA|8|4.7GHz|3.5GHz|NA|NA|12MB|110W|Intel Laminar RM1|$124
Intel Core i5-12400F|NA|6|NA|12|4.4GHz|2.5GHz|NA|NA|18MB|117W|Intel Laminar RM1|$109
Intel Core i3-13100F|NA|4|NA|8|4.5GHz|3.4GHz|NA|NA|12MB|110W|Intel Laminar RM1|$101
Intel Core i3-12100F|NA|4|NA|8|4.3GHz|3.3GHz|NA|NA|12MB|89W|Intel Laminar RM1|$84
</details>

</details>

<details><summary>

### Fans & PC Cooling
</summary>

#### Thermal Compound / Grease
Thermal Compound
:----
Cooler Master MasterGel Regular
Corsair TM30 Performance Thermal Paste

#### CPU Air Coolers
Air Cooler|PWM|Input Voltage|Input Current|Watts|FAN Speed
:----|:----|:----|:----|:----|:----
Thermaltake TOUGHAIR 310|4-pin|12v|0.48A|5.76W|2000RPM

#### Water / Liquid Cooling
Liquid Cooller|Radiator Fan Quantity|Fan Voltage|Pump Voltage|TDP|PWM|Pump Connector|RGB|OpenRGB(using MB)|Pump Power|Radiator Size|Fan Current|Speed
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
Cooler Master MasterLiquid ML 120L V2 RGB (with LGA 1700 Bracket & Backplate)|1|12V|12V|180W|4-pin|3-pin|Yes|Yes|2.36W|120mm|0.15A|1800RPM
Cooler Master MasterLiquid ML240L RGB V2 (with LGA 1700 Bracket & Backplate)|2|12V|12V|180W|4-pin|3-pin|Yes|Yes|2.36W|240mm|0.15A|1800RPM

#### Case Fans
Case Fans|Size|Bearing|PWM|Speed|Fan Voltage|Fan Current|Fan Power|LED Voltage|LED Current|LED Profile|OpenRGB(using MB)
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
XPG Vento 120 ARGB|120mm|Rifle|3-pin|1200RPM|12V|0.16A|1.92W|5V|0.30A|Addressable RGB|Yes

</details>

<details><summary>

### Memory
</summary>

DDR5 RAM|Capacity|Speed|CAS Latency (CL)|XMP|RGB|OpenRGB(using MB)
:----|:----|:----|:----|:----|:----|:----
Crucial DDR5-4800 UDIMM|8GB/ 16GB/ 32GB|4800MHz|-|Yes|NA|NA
Corsair VENGEANCE DDR5 DRAM CL40 Memory Kit|8GB/ 16GB/ 32GB/ 48GB|4800MHz/ 5200MHz/ 5600MHz|40|Yes|NA|NA
Kingston Fury Beast DDR5 Non ECC DIMM|8GB/ 16GB /32GB/ 48GB|4800MHz/ 5200MHz/ 5600MHz|38/ 40|Yes|NA|NA
Kingston Fury Beast RGB DDR5 Non ECC DIMM|8GB/ 16GB /32GB/ 48GB|4800MHz/ 5200MHz/ 5600MHz|38/ 40|Yes|Yes|Yes

DDR4 RAM|Capacity|Speed|XMP|RGB|OpenRGB(using MB)
:----|:----|:----|:----|:----|:----
Crucial DDR4-3200 UDIMM|8GB/ 16GB|3200MHz|-|NA|NA
G.SKILL Ripjaws  DDR4|8GB/ 16GB/ 32GB|3200MHz|Yes|NA|NA
G.SKILL Trident Z DDR4|8GB/ 16GB/ 32GB|3200MHz|Yes|Yes|Yes
</details>

<details><summary>

### Storage
</summary>

Gen 4 M.2 NVMe SSD|Capacity|Read|Write|Form Factor
:----|:----|:----|:----|:----
Crucial P3 Plus|500GB/ 1TB/ 2TB/ 4TB|5000MB/s|4200MB/s|2280
WD Black SN850 NVMe SSD|500GB/ 1TB/ 2TB|7000MB/s|5300MB/s|2280
Corsair Force MP600 Gen.4 PCle|500GB/ 1TB/ 2TB|4950MB/s|4250MB/s|2280
Sabrent Rocket 4 Plus SSD|500GB/ 1TB/ 2TB/4TB|7000MB/s|5800MB/s|2280
Corsair MP600 MINI 1TB (Gen4) PCIe x4 NVMe M.2 2230 SSD|1TB/ 2TB|7000MB/s|6200MB/s|2230
WD_BLACK SN770M NVMe SSD|500GB/ 1TB/ 2TB|5150MB/s|4900MB/s|2230

Gen 3 M.2 NVMe SSD|Capacity|Read|Write|Form Factor
:----|:----|:----|:----|:----
Crucial P1|500GB/ 1TB/ 2TB|2000MB/s|1700MB/s|2280
WD Blue SN570 NVMe SSD| 250GB/ 500GB/ 1TB/ 2TB|3500MB/s|1200MB/s|2280
WD Blue SN550 NVMe SSD|250GB/ 500GB/ 1TB|2400MB/s|1750MB/s|2280
WD Black SN750 NVMe SSD|250GB/ 500GB/ 1TB/ 2TB|3100MB/s|1600MB/s|2280
Crucial P3|500GB/ 1TB/ 2TB/ 4TB|3500MB/s|3000MB/s|2280
Sabrent Rocket NVMe PCIE 3.0 SSD|256GB/ 512GB/ 1TB/ 2TB|3400MB/s|3000MB/s|2280

SATA SSD|Capacity|Form Factor
:----|:----|:----
WD Blue SA510 SATA SSD 2.5”/7mm|250GB/ 500GB/ 1TB/ 2TB/ 4TB|2.5”
Crucial MX500 SSD|250GB/ 500GB/ 1TB/ 2TB/ 4GB|2.5”
Kingston A400 SATA SSD|240GB/ 480GB/ 960GB|2.5”
Crucial BX500 SSD|240GB/ 480GB/ 1TB/ 2TB/ 4TB|2.5”

NVMe M.2 SSD to PCIe Adapter|PCIe|Sizes|Heatsink
:----|:----|:----|:----
Sabrent NVMe M.2 SSD to PCIe X16/X8/X4 Card|X16/X8/X4|2230/2280|Including

M.2 NVMe SSD Enclosure|Size|Type-C
:----|:----|:----
Sabrent USB-C Enclosure for M.2 2230 PCIe NVMe SSDs|2230|USB 3.2 Gen 2

</details>

<details><summary>

### Wi-Fi & Bluetooth Card/Module/Adapter
</summary>

Model|WiFi|Bluetooth|Speed|Card|Interface|NotWorkig
:----|:----|:----|:----|:----|:----|:----
Fenvi FV-T919 (BCM94360)|5|4|1750Mbps|Yes|PCIex1|SIP, FileVault
Fenvi BCM94360NG|5|4|1750Mbps|Module|M.2 A/E|SIP, FileVault
Intel AX101NGW|6|5.2|600Mbps|Module|M.2 E|AirDrop
Intel AX200NGW|6|5.2|2.4Gbps|Module|M.2 A/E|AirDrop
Intel AX201NGW|6|5.2|2.4Gbps|Module|M.2 E|AirDrop
Intel AX210NGW|6E|5.3|2.4Gbps|Module|M.2 A/E|AirDrop
Intel AX211NGW|6E|5.3|2.4Gbps|Module|M.2 E|AirDrop
Intel AX411NGW|6E|5.3|3Gbps|Module|M.2 E|AirDrop
Intel BE200NGW|7|5.4|5.8Gbps|Module|M.2 E|AirDrop, 6GHz
Intel BE202NGW|7|5.4|2.4Gbps|Module|M.2 E|AirDrop, 6GHz
TPLink Archer T2U NANO|5|NA|433Mbps|Adapter|USB|AirDrop
DLink DWA131E 92EU|4|NA|300Mbps|Adapter|USB|AirDrop
Realtek RTL8812BU|5|NA|1200Mbps|Adapter|USB|AirDrop

</details>

<details><summary>

### PC chassis
</summary>

Chassis|MB|Front Cooling Fan|Top Cooling Fan|Rear Cooling Fan|Front Pre-Installed Fan|Top Pre-Installed Fan|Rear Pre-Installed Fan|Front Radiator|Top Radiator|Rear Radiator|CPU Cooler|GPU|Storage|USB Type-A|USB Type-C|Audio|Mic|Case Expansion Slots|PSU|Cable Management Space|LED|LED Profile|OpenRGB(using MB)
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
Corsair Carbide Series SPEC-01|Mini-ITX MicroATX ATX|120mm|||120mm|||120mm|||150mm|414mm|4x2.5" + 4x3.5"|||||7|||Yes|NA|NA
MSI MAG FORGE 100M|ATX / Micro ATX/ Mini-ITX|3x120mm|2x120mm|1x120mm|2x120mm RGB|NA|1x120mm|120/ 240mm|120/ 240mm|120/ 240mm|160mm|330mm|3x2.5" + 2x3.5"|2xUSB 3.2 Gen1|NA|1|1|7|ATX 160-200mm|-|RGB|Addressable|Yes
ASUS TUF Gaming GT301|ATX|3x120mm|2x120mm|1x120mm|3x120mm ARGB|NA|1x120mm|360mm|-|120mm|160mm|320mm|4x2.5" + 2x3.5"|2xUSB 3.1 Gen1|NA|1|1|7|ATX 160mm|30mm|ARGB|Addressable RGB|-
NZXT H510|Mini-ITX, MicroATX, ATX|2x120mm|1x120mm|1x120mm|NA|NA|120mm|280mm|NA|120mm|165mm|381mm|3x2.5" + 3x2.5"|USB 3.2 Gen 1|USB 3.2 Gen 2|1|1|7|-||23mm|||
Fractal Design Meshify C|ATX, mATX, ITX|3x120mm|2x120mm|1x120mm||||360mm|240mm|120mm|170mm|315mm|3x2.5" + 2x3.5"|2xUSB 3.0|NA|1|1|7|175mm|35mm|||

</details>

<details><summary>

### Power supply unit
</summary>

PSU|Watt|Certified|Moduler|ATX(motherboard)|EPS(cpu)|SATA(storage)|PCIe(GPU)|Molex(fan)|RGB|OpenRGB
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
Corsair CV450|450W|80+ Bronze|NA|24-pin|4+4pin|6|2x6+2pin|3|NA|NA
Corsair CX650F RGB|650W|80+ Bronze|Fully|24-pin|4+4pin|7|4x6+2pin|NA|Addressable|-
Corsair RM750|750W|80+ Gold|Fully|24-pin|4+4pin|10|6+2-pin|4|NA|NA
ASUS Rog Strix 750G|750W|80+ Gold|Fully|24-pin|2x4+4-pin|12|12+4-pin & 4x6+2-pin|3|NA|NA
</details>

<details><summary>

### Graphic Card
</summary>

#### Polaris Series

GPU|Variant|Process|Transistors|Generation|Bus Interface|Memory|GPU Bese Clock|GPU Boost Clock|Memory Clock|P|HDMI|DP|Cores|BUS Width|FreeSync|HDR|HDMI Resolution|DP Resolution|Spoof|Boot argument|OS Support|Power Connector|Kext|Architecture|RGB|OpenRGB|Resizable BAR|Partners
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
AMD Radeon RX 550|Lexa|14nm|2200M|Polaris|PCIe 3.0×8|4GB GDDR5|1100MHz|1183MHz|1750MHz|65W|2.0|1.4|512|128bit|Yes|Yes|4096×2160@60Hz|5120x2880@60HZ|FF67|-radcodec|Latest|NA|Lilu+WhateverGreen|GCN 4.0|NA|NA|NA|Sapphire Pulse Radeon RX 550 4GB GDDR5
AMD Radeon RX 560|Polaris 21|14nm|3000M|Polaris|3.0x8|4GB GDDR5|1175MHz|1275MHz|1750MHz|75W|2.0|1.4|1024|128bit|-|-|-|5120x2880@-|NA|-radcodec|Latest|8-pin|WhateverGreen+Lilu|GCN 4.0|Yes|Yes|NA|¹ASUS Dual Radeon RX 560 4GB GDDR5 ²ASUS ROG Strix Radeon RX 560 V2 4GB GDDR5
AMD Radeon RX 570|Polaris 20|14nm|5700M|Polaris|3.0x16|4/8GB GDDR5|1168MHz|1244MHz|1750MHz|150W|2.0|1.4|2048|256bit|Yes|Yes|-|7680x4320@-|NA|-radcodec|Latest|8-pin|WhateverGreen+Lilu|GCN 4.0|NA|NA|NA|ASRock AMD Radeon RX 570 Phantom Gaming Elite 8G

#### Navi 23 Series

GPU|Variant|Process|Transistors|Generation|Bus Interface|Memory|GPU Bese Clock|GPU Boost Clock|Memory Clock|P|HDMI|DP|Cores|BUS Width|FreeSync|HDR|HDMI Resolution|DP Resolution|Spoof|Boot argument|OS Support|Power Connector|Kext|Architecture|Resizable BAR|Partners
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
AMD Radeon RX 6600|Navi 23|7nm|11060M|Navi II|4.0x8|8GB GDDR6|1626MHz|2491MHz|1750MHz|132W|2.1|1.4a|1792|128bit|Yes|-|7680×4320|7680×4320|NA|agdpmod=pikera|Latest|8-pin|LiLu.kext + WhateverGreen.kext|RDNA 2.0|Yes|Sapphire PULSE AMD Radeon RX 6600
AMD Radeon RX 6600 XT|Navi 23|7nm|11060M|Navi II|4.0x8|8GB GDDR6|1968MHz|2589MHz|2000MHz|160W|2.1|1.4a|2048|128bit|Yes|-|7680×4320@-|7680×4320@-|NA|agdpmod=pikera|Latest|8-pin|LiLu.kext + WhateverGreen.kext|RDNA 2.0|Yes|¹Sapphire PULSE AMD Radeon RX 6600 XT ²ASRock AMD Radeon RX 6600 XT Challenger D 8GB OC
AMD Radeon RX 6650 XT|Navi 23|7nm|11060M|Navi II|4.0x8|8GB GDDR6|2055MHz|2635MHz|2190MHz|176W|2.1|1.4a|2048|128bit|Yes|-|7680×4320@-|7680×4320@-|FF730000|agdpmod=pikera|Latest|8-pin|LiLu.kext + WhateverGreen.kext|RDNA 2.0|Yes|Sapphire PULSE AMD Radeon RX 6650 XT

#### Navi 22 Series

GPU|Variant|Process|Transistors|Generation|Bus Interface|Memory|GPU Bese Clock|GPU Boost Clock|Memory Clock|P|HDMI|DP|Cores|BUS Width|FreeSync|HDR|HDMI Resolution|DP Resolution|Spoof|Boot argument|OS Support|Power Connector|Kext|Architecture|Resizable BAR|Partners
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
AMD Radeon RX 6700 XT|Navi 22|7nm|17200M|Navi II|4.0x16|12GB GDDR6|2321MHz|2581MHz|2000MHz|230W|2.1|1.4a|2560|192bit|Yes|-|7680×4320@-|7680×4320@-|NA|NA|Latest|1x8-pin + 1x6-pin|Lilu.kext + NootRX.kext|RDNA 2.0|Yes|Sapphire PULSE AMD Radeon RX 6700 XT

#### Navi 21 Series

GPU|Variant|Process|Transistors|Generation|Bus Interface|Memory|GPU Bese Clock|GPU Boost Clock|Memory Clock|P|HDMI|DP|Cores|BUS Width|FreeSync|HDR|HDMI Resolution|DP Resolution|Spoof|Boot argument|OS Support|Power Connector|Kext|Architecture|RGB|OpenRGB|Resizable BAR|Partners
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
AMD Radeon RX 6800|Navi 21|7nm|26800M|Navi II|4.0x16|16GB GDDR6|1700MHz|2105MHz|2000MHz|250W|2.1|1.4a|3840|256bit|-|-|4K@120Hz|7680x4320@-|NA|agdpmod=pikera|Latest|3x8-pin|WhateverGreen.kext + Lilu.kext|RDNA 2.0|Yes|Yes|Yes|MSI Radeon RX 6800 GAMING X TRIO 16G
AMD Radeon RX 6800 XT|Navi 21|7nm|26800M|Navi II|4.0x16|16GB GDDR6|1825MHz|2250MHz|2200MHz|300W|2.1|1.4a|4608|256bit|Yes|-|-|7680x4320@-|NA|agdpmod=pikera|Latest|3x8-pin|WhateverGreen.kext + Lilu.kext|RDNA 2.0|Yes|Yes|Yes|ASRock AMD Radeon RX 6800 XT Phantom Gaming D 16G OC
AMD Radeon RX 6900 XT|Navi 21|7nm|26800M|Navi II|4.0x16|16GB GDDR6|1825MHz|2250MHz|2000MHz|300W|2.1|1.4a|5120|256bit|Yes|-|-|7680x4320@-|NA|agdpmod=pikera|Latest|3x8-pin|WhateverGreen.kext + Lilu.kext|RDNA 2.0|Yes|-|Yes|ASRock AMD Radeon RX 6900 XT Phantom Gaming D 16G OC
AMD Radeon RX 6950 XT|Navi 21|7nm|26800M|Navi II|4.0x16|16GB GDDR6|1860MHz|2310MHz|2250MHz|335W|2.1|1.4a|5120|256bit|Yes|-|7680×4320@-|7680×4320@-|BF730000|agdpmod=pikera|Latest|2x8-pin + 1x6-pin|NootRx.kext + Lilu.kext|RDNA 2.0|Yes|Yes|Yes|Sapphire NITRO+ AMD Radeon RX 6950 XT

</details>

<details><summary>

### Monitor
</summary>

Monitor|Resolution|Size|Frame|DDC/CI|Vertical Mode|Speaker|Brightness|Response Time|HDMI|DP|IPS|HDR|FreeSync|Anti Glare|LED Backlight|Ambient Sensor|Type-C|Camera|Mic
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
BenQ GW2283|1080p|21.5"|60Hz|Yes|NA|2x1W|250Nits|5ms|2xv1.4|NA|Yes|NA|NA|Yes|Yes|Yes|NA|NA|NA
Acer Nitro VG240YB|1080p|23.8"|75Hz|Yes|NA|2x2W|250Nits|1Ms|2x|NA|Yes|NA|Yes|Yes|Yes|NA|NA|NA|NA
BenQ Pd2500Q|2K|25"|60Hz|Yes|Yes|2x4W|350Nits|4ms|1xv1.4|1xv1.2|Yes|NA|NA|Yes|Yes|Yes|NA|NA|NA
LG 27UL500-W|4K|27"|60Hz|Yes|NA|NA|300Nits|5ms|2x|1xv1.4|Yes|10|Yes|Yes|Yes|NA|NA|NA|NA
BenQ Pd2700U|4K|27"|60Hz|Yes|Yes|2x2W|350Nits|5ms|1xv2.0|1xv1.4|Yes|10|NA|Yes|Yes|Yes|NA|NA|NA
LG 27MD5KL-B|5K|27"|60Hz|Yes|NA|2x5W|500Nits|14ms|NA|NA|Yes|Yes|Yes|Yes|Yes|NA|3xUSB-C 1xThunderbolt 3|1080p@30fps|Yes
</details>

<details><summary>

### Mouse & Keyboard
</summary>

Mouse|Wireless|RGB|OpenRGB|DPI|Back/Forward|Rechargeable Battery|Charging Port|Braided Cable
:----|:----|:----|:----|:----|:----|:----|:----|:----
Zebronics Zeb-Transformer-M - Premium Gaming Mouse|NA|Yes|NA|3600|Yes|NA|NA|Yes
Redragon Cobra M711|NA|Yes|Yes|10000|Yes|NA|NA|Yes
Offbeat Ripjaws Wireless Gaming Mouse|2.4GHz|Yes|NA|3200|Yes|Yes|MicroUSB|NA
Redragon Trident Pro M693 RGB|2.4GHz/ BT@-|Yes|Yes|4000|Yes|Yes|Type-C|NA

Keyboard|Wireless|Machanical|Switch|RGB|OpenRGB|Rechargeable Battery|Port|USB Cable|QMK Firmware|Tenkeyless (Compact)|Arrow/ Delete keys (Dedicated)|Hot-Swappable Switches (Replacement)
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
HP K300|NA|NA|Membrane|Yes|NA|NA|NA|NA|NA|NA|Yes|NA
Redragon Fizz K617 Black|NA|Yes|Red|Yes|NA|NA|NA|NA|Yes|Yes|NA|Yes
Redragon Kumara K552-Rainbow Black|NA|Yes|Red|Yes|NA|NA|NA|NA|Yes|Yes|Yes|Yes
Portronics Hydra 10|2.4GHz/ BT5.0|Yes|Red|Yes|-|1A|Type-C|Yes|Yes|Yes|Yes|NA
Redragon Kumara K552-RGB Black|NA|Yes|Blue|Yes|Yes|NA|NA|NA|Yes|Yes|Yes|Yes
Redragon Diemos K599-RGB|2.4GHz|Yes|Blue|Yes|Yes|Yes|USBType-C|NA|NA|Yes|Yes|Yes
HP HyperX Alloy Origins Core|NA|Yes|-|Yes|Yes|NA|Type-C|Yes|NA|Yes|Yes|Yes
ROYAL KLUDGE RK84|2.4GHz/ BT5.0|Yes|Red|Yes|-|3.7A|Type-C|Yes|Yes|Yes|Yes|Yes

Keyboard Mechanical Switches

Switch Type|Pin|KeyCaps|Actuation Force|Switch Design|Noise Level|Use Case|Quality|Price|Durability|Buy
:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----
Cherry MX Blue||||||||||
Cherry MX Red|5-pin|+|Low|Linear|Quiet|Gaming|Highest|Highest|Highest|[cosmicbyte](https://www.thecosmicbyte.com/product/cherry-mx-mechancial-5-pin-switches-compatible-with-hot-swappable-keyboards-pack-of-10/)
Cherry MX Brown||||||||||
Gateron Blue|3-pin/ 5-pin|[(+)]/ +|High|Clicky|Audible|Typing|High|Mid-range|High|[cosmicbyte](https://www.thecosmicbyte.com/product/gateron-mechanical-switches-compatible-with-cosmic-byte-hot-swappable-keyboards-qty-1pc/)
Gateron Red|3-pin/ 5-pin|[(+)]/ +|Low|Linear|Quiet|Gaming|High|Mid-range|High|[cosmicbyte](https://www.thecosmicbyte.com/product/gateron-mechanical-switches-compatible-with-cosmic-byte-hot-swappable-keyboards-qty-1pc/)
Gateron Brown||||||||||
Outemu Blue|3-pin|[+]/ +|High|Clicky|Audible|Typing|Decent|Lowest|Moderat|[cosmicbyte]()
Outemu Red|3-pin|[+]/ +|Low|Linear|Quiet|Gaming|Decent|Lowest|Moderat|[cosmicbyte](https://www.thecosmicbyte.com/product/outemu-mechanical-switches-for-swappable-keyboards-pack-of-20/)
Outemu Brown|3-pin|[+]/ +|Mid|Tactile|Moderate|Both Typing & Gaming|Decent|Lowest|Moderat|[cosmicbyte](https://www.thecosmicbyte.com/product/outemu-mechanical-switches-for-swappable-keyboards-pack-of-20/)

</details>

<details><summary>

### UPS
</summary>

UPS|Capacity|SineWave
:----|:----|:----
Luminous Home UPS 900VA Zelio+ 1100|900VA|Yes

+

UPS Battery|Capacity|Type
:----|:----|:----
Lominous Battery 120 Ah - RC15000|120Ah|Tubular
Lominous Battery 150 Ah - RC18000ST|150Ah|Tubular

</details>

<details><summary>

### Accessories
</summary>

#### WebCam

WebCam|Resolution|Frame|Mic|Flash|Privacy Shutter
:----|:----|:----|:----|:----|:----
Logitech C270 HD Webcam|720p|30fps|Yes|-|Yes
Logitech Brio 100 Full HD Webcam|1080p|30fps|Yes|-|Yes
Logitech C920 HD Pro Webcam|1080p|30fps|Yes|-|-
Logitech Brio Stream Ultra HD Webcam|4k|90fps|Yes|-|-

#### Speaker

Speaker|Watt|Bluetooth
:----|:----|:----
BoAt Stone 650|10W|5
Logitech Z623 THX 400 Watt 2.1 Channel Wired Speaker|400W|NA

#### Headphone

Headphone|Driver Size|Bluetooth
:----|:----|:----
BoAt BassHeads 225|10mm|NA
Boat Airdopes 141|8mm|5
BoAt Rockerz 510|50mm|4.1

#### Splitter

3.5mm Headphone 2 Male to 1 Female 3.5mm Headphone Mic

Cooler Master Addressable RGB 1-to-5 Splitter Cable – ARGB

#### Flash Drive
Drive|Capacity|Read|Write|USB|TypeC
:----|:----|:----|:----|:----|:----
SanDisk Ultra Dual USB Drive 3.1|16/ 32/ 64/ 128/ 256GB|150MBps|30MBps|3.1|Yes

USB GPS|communication protocols|Official Driver|Third-Party Drivers
:----|:----|:----|:----
GlobalSat BU-353-S4|NMEA|[BU-353S4](https://www.globalsat.com.tw/en/a4-10593/BU-353S4.html)|[GPSD](https://formulae.brew.sh/formula/gpsd#default)/ [GPXSee](https://sourceforge.net/projects/gpxsee/files/Mac%20OS%20X/)/ [KisMac2](https://igrsoft.com/beta/KisMac2.zip)/ [QGIS](https://qgis.org/download/)/ [OpenCPN](https://opencpn.org/OpenCPN/info/downloadopencpn.html)

</details>

### Suggested PC Hardware:

PC|min|Low-Level (Budget-Focused)|Mid-Level|High-Level (Content Creation)
:----|:----|:----|:----|:----
CPU|Intel Core i3-12100F|Intel Core i5-12400F|Intel Core i7-13700KF|Intel Core i9-13900KF
GPU|AMD Radeon RX 560|AMD Radeon RX 6600 or RX 6600 XT or RX 6650 XT|AMD Radeon RX 6700 XT or 6750 XT|AMD Radeon RX 6900 XT or RX 6950 XT
Motherboard|GIGABYTE B760M DS3H AX DDR5|MSI MAG B760M Mortar WiFi|ASUS TUF Gaming Z790-Plus WiFi|ASUS ProArt Z790 Creator WiFi
RAM|Crucial 8GB (1x8GB) DDR5-4800|Corsair VENGEANCE 16GB (1x16GB) DDR5 DRAM 5600MT/s CL40 Memory Kit|Corsair VENGEANCE 32GB (1x32GB) DDR5 DRAM 5600MT/s CL40 Memory Kit|Kingston Fury Beast RGB 64GB (2x32GB) DDR5 5600MT/s CL40 Non ECC DIMM
Storage|WD Blue SN570 500GB|WD Black SN750 1TB|WD Black SN850 2TB|Sabrent Rocket 4 Plus SSD 4TB
Case|MSI MAG FORGE 100M|MSI MAG FORGE 100M|MSI MAG FORGE 100R|NZXT H510
PSU|Corsair CX550M|Corsair CX650M|Corsair RM750|Corsair RM850x
Cooling|Stock Cooler (Intel Laminar RM1)|Stock Cooler (Intel Laminar RM1)|Cooler Master MasterLiquid ML240L RGB V2|Cooler Master MasterLiquid ML240L RGB V2
Thermal Compound|pre-applied on stock cooler|pre-applied on stock cooler|Cooler Master MasterGel Regular|Corsair TM30 Performance Thermal Paste
Case Fans|1x XPG Vento 120 ARGB (Optional)|1x XPG Vento 120 ARGB (Optional)|1x XPG Vento 120 ARGB (Optional)|-
Monitor|Acer Nitro VG240YB|BenQ Pd2500Q|BenQ Pd2700U|LG 27MD5KL-B
Wi-Fi & Bluetooth (Optional)|BCM94360 / FV-T919|BCM94360 / FV-T919|BCM94360 / FV-T919|BCM94360 / FV-T919
Keyboard|Redragon Fizz K617 Black|Redragon Kumara K552-Rainbow Black|Redragon Kumara K552-RGB Black|ROYAL KLUDGE RK84
Mouse|Zebronics Zeb-Transformer-M - Premium Gaming Mouse|Redragon Cobra M711|Redragon Cobra M711|Redragon Trident Pro M693 RGB
macOS Compatibility|Tahoe|Tahoe|Tahoe|Tahoe
UPS & Battery (Optional)|Luminous Home UPS 900VA Zelio+ 1100 & Lominous Battery 120 Ah|Luminous Home UPS 900VA Zelio+ 1100 & Lominous Battery 120 Ah|Luminous Home UPS 900VA Zelio+ 1100 & Lominous Battery 150 Ah|Luminous Home UPS 900VA Zelio+ 1100 & Lominous Battery 150 Ah
WebCam (Optional)|Logitech C270 HD Webcam|Logitech Brio 100 Full HD Webcam|Logitech C920 HD Pro Webcam|Logitech Brio Stream Ultra HD Webcam
Splitter (Optional)|3.5mm Headphone 2 Male to 1 Female 3.5mm Headphone Mic / Cooler Master Addressable RGB 1-to-5 Splitter Cable – ARGB|3.5mm Headphone 2 Male to 1 Female 3.5mm Headphone Mic / Cooler Master Addressable RGB 1-to-5 Splitter Cable – ARGB|3.5mm Headphone 2 Male to 1 Female 3.5mm Headphone Mic / Cooler Master Addressable RGB 1-to-5 Splitter Cable – ARGB|3.5mm Headphone 2 Male to 1 Female 3.5mm Headphone Mic / Cooler Master Addressable RGB 1-to-5 Splitter Cable – ARGB
Flash Drive (Optional)|SanDisk Ultra Dual USB Drive 3.1|SanDisk Ultra Dual USB Drive 3.1|SanDisk Ultra Dual USB Drive 3.1|SanDisk Ultra Dual USB Drive 3.1
Spec|Support 4x64GB=256GB DDR5 4800MHz Memory (also depand on CPU)|Support 4x64GB=256GB DDR5 5600MHz Memory (also depand on CPU)|Support 4x32GB=128GB DDR5 5200MHz Memory or  4x48GB=192GB DDR5 5600MHz Memory (also depand on CPU)|Support 4x32GB=128GB DDR5 5200MHz Memory or  4x48GB=192GB DDR5 5600MHz Memory (also depand on CPU)

</details>

<details><summary>

## 📦Pre-built EFI
</summary>

install [pv](https://formulae.brew.sh/formula/pv)
```
brew install pv
```
login
```
sudo -i "id"
```
mount system EFI partition
```
sudo diskutil mount EFI 
```
create zip archive
```
OC=$(nvram 4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102:opencore-version 2>&1 | grep -o 'REL-[0-9]*' | awk -F'-' '{v=$2; print substr(v,1,1)"."substr(v,2,1)"."substr(v,3,2)}'); macOS=$(sw_vers -productVersion); date=$(date +"%Y.%m.%d.%H.%M"); bsdtar --format=zip -c -f - -C "/Volumes/EFI/EFI" . | pv -t -b -r > "$HOME/Downloads/EFI_$macOS-$OC-$date.zip"
```
unmount system EFI partition
```
sudo diskutil unmount /Volumes/EFI
```
view archive content
```
OC=$(nvram 4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102:opencore-version 2>&1 | grep -o 'REL-[0-9]*' | awk -F'-' '{v=$2; print substr(v,1,1)"."substr(v,2,1)"."substr(v,3,2)}'); macOS=$(sw_vers -productVersion); bsdtar -tf "$HOME/Downloads/"EFI_$macOS-$OC-*.zip
```
extract archive
```
OC=$(nvram 4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102:opencore-version 2>&1 | grep -o 'REL-[0-9]*' | awk -F'-' '{v=$2; print substr(v,1,1)"."substr(v,2,1)"."substr(v,3,2)}'); macOS=$(sw_vers -productVersion); mkdir -p "$HOME/Downloads/EFI" && pv "$HOME/Downloads/"EFI_$macOS-$OC-*.zip | bsdtar -xf - -C "$HOME/Downloads/EFI"
```
remove EFI zip archive file (if needed)
```
OC=$(nvram 4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102:opencore-version 2>&1 | grep -o 'REL-[0-9]*' | awk -F'-' '{v=$2; print substr(v,1,1)"."substr(v,2,1)"."substr(v,3,2)}'); macOS=$(sw_vers -productVersion); rm -f "$HOME/Downloads/"EFI_$macOS-$OC-*.zip
```
remove extracted EFI folder (if needed)
```
rm -rf "$HOME/Downloads/EFI"
```
clear
```
printf '\033[2J\033[3J\033[H'
```
[Download](https://github.com/arghya339/some-stupid-thing/releases/tag/OpenCore)
</details>

<details><summary>


## 🚩Related Repo
</summary>

- [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/): Official OpenCore install Guide for 1st/2nd/3rd/5th/6th/7th/9th/10th-Gen Intel CPU by Dortania.
- [OpenCore Legacy Patcher(OCLP)](https://dortania.github.io/OpenCore-Legacy-Patcher/MODELS.html): install newer versions of macOS on older Supported Macs that Apple officially no longer supports, using [this](https://github.com/dortania/OpenCore-Legacy-Patcher) fantastic tool.
- [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools): GUI-based Configurator for editing `config.plist` files + [Config_Templates.zip](https://github.com/5T33Z0/OC-Little-Translated/blob/main/F_Desktop_EFIs/Config_Templates/Config_Templates.zip): Intel CPU Configuration template (1st~11th-Gen Intel CPU) for OCAuxiliaryTools by [5T33Z0](https://github.com/5T33Z0) + [OpenCore Visual Beginners Guide](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/step-by-step/oc-auxiliary-tools): OpenCore Auxiliary Tools User's Guide by [ChrisWayg]().
- [Ryzentosh](https://github.com/mikigal/ryzen-hackintosh): Hackintosh for AMD Ryzen based systems.
- [OSX-Hyper-V](https://github.com/Qonfused/OSX-Hyper-V): macOS on Windows Hyper-V + [MacHyperVSupport](https://github.com/acidanthera/MacHyperVSupport): Hyper-V integration for macOS. [Guide](https://elitemacx86.com/threads/how-to-install-macos-on-hyper-v-opencore-install-guide.1443/)
- [Install Windows/ Linux using Android](https://github.com/arghya339/some-stupid-thing/blob/main/Install-Windows-Linux-using-Android.md)
- [open-source-mac-os-apps](https://github.com/serhii-londar/open-source-mac-os-apps): Awesome list of open source applications for macóS.
</details>

<details><summary>
    
## 🫡Credits
</summary>
Thanks to:

- [Acidanthera](https://github.com/acidanthera)
- [Apple](https://www.apple.com/mac/)
- [r/hackintosh](https://www.reddit.com/r/hackintosh/)
- [ChrisWayg](https://www.reddit.com/r/hackintosh/comments/sp1zgv/opencore_alder_lake_12thgen_intel_hackintosh/) 
- [serhii-londar](https://github.com/serhii-londar/open-source-mac-os-apps)
- [MSTRKKRFT](https://www.reddit.com/r/hackintosh/comments/npvuqg/hackintosh_macos_free_tools/)
- [basic-writing-and-formatting-syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

by [@arghya339](https://github.com/arghya339)
</details>

<details><summary>

## 💌Support
</summary>

- Donation: [PayPal/@arghyadeep339](https://www.paypal.com/paypalme/arghyadeep339)
- Subscribe: [YouTube/@MrPalash360](https://www.youtube.com/channel/UC_OnjACMLvOR9SXjDdp2Pgg/videos?sub_confirmation=1)
- Follow: Telegram
- Join: Telegram
</details>

# I ❤️ [Unix-like](https://en.wikipedia.org/wiki/Unix-like)
