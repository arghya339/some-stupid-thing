# OPPO A37fw Software Upgrade Guide

> FOR OPPO A37FW ONLY (NOT A37 AND NOT A37F AND NOT FOR ANY OTHER DEVICES)

> WARNING: I DO NOT OWN ANYTHING AND THIS GUIDE IS JUST MY EXPERIENCE IN SOFTWARE UPGRADE AND FOR THOSE WHO HAD HARD TIME TO UPGRADE THEIR A37FW DEVICES LIKE ME, I AM NOT RESPONSIBLE TO ANY DAMAGE YOU GOT, SO TAKE IT AS YOUR OWN RISK.

## System Requirements

- Windows 10 or Later

## Preparing

- [Qualcomm](https://qcomdriver.com/) USB Drivers
- [android-platform-tools](https://wiki.lineageos.org/adb_fastboot_guide#on-windows)
- [Stock ROM](https://firmwareos.com/oppo-a37fw) Use to fix softbrike(bootloop)
- [Modified Stock ROM](https://github.com/arghya339/some-stupid-thing/releases/download/OPPO-A37FW/A37fwEX_11_A.22_170522.Modified.zip) Use the A37fwEX_11_A.22_170522 build number(17xxxx Modified is bootloader unlock possible)
- [BootUnlocker.zip](https://github.com/arghya339/some-stupid-thing/releases/download/OPPO-A37FW/BootUnlocker.zip)
- [prog-emmc-firehose-8936.mbn](https://github.com/arghya339/some-stupid-thing/releases/download/OPPO-A37FW/prog_emmc_firehose_8936.mbn)
- [HexEiditor](https://hhdsoftware.com/free-hex-editor)
- [TWRP](https://sourceforge.net/projects/meghbuilds/files/twrp_A37_3.7.img/download)
- [lineage-17.1-20220328-UNOFFICIAL-A37_gms_go.zip](https://github.com/arghya339/some-stupid-thing/releases/download/OPPO-A37FW/lineage-17.1-20220328-UNOFFICIAL-A37_gms_go.zip)
- [open_gapps-arm-10.0-pico-20220215.zip](https://sourceforge.net/projects/opengapps/files/arm/20220215/open_gapps-arm-10.0-pico-20220215.zip/download)
- [Magisk](https://github.com/topjohnwu/Magisk/releases/download/v26.4/Magisk-v26.4.apk)
- [PlayIntegrityFix](https://github.com/chiteroman/PlayIntegrityFix/releases/)
> They have their own guide in the links to install, please follow them correctly.

## Software Downgrading

> As you can see, i am using `Msm8x39DownloadTool.exe` because it's detecting my device.

- Download & extract the [Modified Stock ROM](https://github.com/arghya339/some-stupid-thing/releases/download/OPPO-A37FW/A37fwEX_11_A.22_170522.Modified.zip)
- Connect your device(A37FW) in EDL mode:

   - just tap 5-7 time on Build Number (you can find build number in `About Phone`)

   - then turn on `Developer Option` > enter `Developer Mode` > turn on `USB Debugging`

   - then run following command in Windows Power Shell:

      ~ adb devices

      ~ adb reboot edl

- then run `Msm8x39DownloadTool.exe` as an administrator.

 > make sure you have setup [`android-platform-tools`](https://wiki.lineageos.org/adb_fastboot_guide#on-windows)
 
  > Windows `Devices Manager` will show your devices(OPPO A37FW) Connected the COM Port
 
 > Note: after sucessfully downgrade to your devices software your device atomatically reboot to Phone Setup

## Unlocking Bootloader

> Oppo a37fw bootloader is already locked when you follow this guide so you can modify your system as much as you want(flash twrp, custom roms, custom kernel and more).

- Download and extract [BootUnlocker.zip](https://github.com/arghya339/some-stupid-thing/releases/download/OPPO-A37FW/BootUnlocker.zip)

- Download [prog-emmc-firehose-8936.mbn](https://github.com/arghya339/some-stupid-thing/releases/download/OPPO-A37FW/prog_emmc_firehose_8936.mbn)

- go `BootUnlocker` extracted folder

- move `prog-firehose-emmc-8936.mbn` to your `BootUnlocker` extracted folder
- Connect your device(OPPO A37FW) in EDL mode
- open Windows `Decice Manager` > under `Ports (COM & LPT)` > `Qualcomm HS-USB QDLoader 9008 (COM4)

  > NOTE: your device connected COM PORT Number for my case 4 (COM4)

- go back to `BootUnlocker` extracted folder and double click & run `dump_devinfo.bat` file

  - Enter the port number your device id connected to: `COM4` (for my case COM4)

  - Enter the fulll path of your (prog-emmc-firehose-8936.mbn) firehose file : C:\Users\YourUserName\Download\BootUnlocker\prog-emmc-firehose-8936.mbn

   - Download, extract and install [HexEiditor](https://hhdsoftware.com/free-hex-editor) on your Windows

  - right click on `devinfo.img` > `Open with` > `HxD Hex Editor`

    - change following Hex code:

      - (900000010,00) = 00 -> FF

      - (900000010,08) = 00 -> FF

    -  then press `Ctrl` + `S` on your keyboard.

   - go back to `BootUnlocker` extracted folder and double click & run `unlock.bat`

   - Enter the port number your device is connected to : `COM4` (for my case COM4)
   
   - Enter the full path of your (prog-emmc-firehose-8936.mbn) filehose file : C:\Users\YourUserName\Download\BootUnlocker\prog-emmc-firehose-8936.mbn
   
   - Press any key to continue ... > press f and hit Enter
   
   - Now you see `Bootlaoder Unlock Complited` messages
   
   - power on your phone by `Long press power button`.

## Flash TWRP & LineageOS 17 (Android 10)
  
  - Download [TWRP for A37](https://sourceforge.net/projects/meghbuilds/files/twrp_A37_3.7.img/download)
  
  - Download [lineage-17.1-20220328-UNOFFICIAL-A37_gms_go.zip](https://github.com/arghya339/some-stupid-thing/releases/download/OPPO-A37FW/lineage-17.1-20220328-UNOFFICIAL-A37_gms_go.zip)

  - Download [open_gapps-arm-10.0-pico-20220215.zip](https://sourceforge.net/projects/opengapps/files/arm/20220215/open_gapps-arm-10.0-pico-20220215.zip/download)

  - Connect your device to Computer using USB cable
  
  - turn on USB Debugging on your phone
 
  - set up [android-platform-tools](https://wiki.lineageos.org/adb_fastboot_guide#on-windows)
 
  - Open Windows Power Shell & run following commands:
   
    ~ adb devices
   
    ~ adb reboot bootloader
    
    ~ fastboot devices
    
    ~ fastboot flash recovery C\:Users\YourUserName\Download\twrp_A37_3.7.img
    
    ~ fastboot reboot recovery
 
 - TWRP > Wipe > wipe data, cache, system, boot, delvik-cache
 
 - TWRP > Advanced > ADB Sideload

 - Open Windows Power Shell & run following commands:
   
   ~ adb sideload C\:Users\YourUserName\Download\lineage-17.1-20220328-UNOFFICIAL-A37_gms_go.zip

 - TWRP > Reboot > Recovery

 - TWRP > Advanced > ADB Sideload

 - Open Windows Power Shell & run following commands:
   
   ~ adb sideload C\:Users\YourUserName\Download\open_gapps-arm-10.0-pico-20220215.zip

 - TWRP > Reboot > System 
 
 - Setup your Phone 

## Rooting & Fix Device Uncertified

 - Download & extract [lineage-17.1-20220328-UNOFFICIAL-A37_gms_go.zip](https://github.com/arghya339/some-stupid-thing/releases/download/OPPO-A37FW/lineage-17.1-20220328-UNOFFICIAL-A37_gms_go.zip)

 - go to lineage-17.1-20220328-UNOFFICIAL-A37_gms_go extracted folder

 - Copy boot.img form lineage-17.1-20220328-UNOFFICIAL-A37_gms_go.zip extracted folder to your phone Download folder using USB file transfer
 
 - Download & install [Magisk.apk](https://github.com/topjohnwu/Magisk/releases/download/v26.4/Magisk-v26.4.apk) on your phone
 
 - Open Magisk
  
   - Install 

   - Select and Patch a File

   - Select OPPO A37/Download/boot.img

   - LET'S GO
   
 - Copy OPPO A37/Download/MagiskPatch-boot.img from your phone to Computer C:\Users\YourUserName\Download folder using USB file transfer

 - turn on Developer Options & USB Debugging on your phone
 
 - set up [android-platform-tools](https://wiki.lineageos.org/adb_fastboot_guide#on-windows)

 - Open Windows Power Shell and run following commands:
   
   ~ adb devices
   
   ~ adb reboot bootloader
   
   ~ fastboot devices
   
   ~ fastboot flash boot C:\Users\YourUserName\Download\MagiskPatch-boot.img
   
   ~ fastboot reboot

 - Open Magisk > Reboot
 
 - Open Magisk > Settings > Turn on Zygisk, Enforce DenyList.
 
 - Download & flash [PlayIntegrityFix.zip](https://github.com/chiteroman/PlayIntegrityFix/releases/) form Magisk > Module > Install from Storage
 
 - Reboot your device

 - Open Magisk > Settings > Configure DenyList > switch on Financial app (ie. PNB ONE, Airtel, MyJio, BHIM, GPay, Amazon Pay, PhonePe, Paytm, FreeCharge, MobiKwik, PayPal, ZebPay etc)

 
 - Now you can use any financial app (ie. PhonePe) without any issues.

> Note: After Passing Device Certified by fixing play integrity using Magisk, you can't use iMobile Pay on your device!
