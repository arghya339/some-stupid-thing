# Install Windows/ Linux using Android

## Download Ubuntu ISO:
- [Download Ubuntu Desktop](https://ubuntu.com/download/desktop)
- [Alternative downloads](https://ubuntu.com/download/alternative-downloads)
- [Ubuntu 23.04 (Lunar Lobster)](https://old-releases.ubuntu.com/releases/lunar/)

- if you are using x86 arch computer download `amd64.iso` file

- if you need high download speed download `amd64.iso.torrent` and add to [Bittorrent](https://play.google.com/store/apps/details?id=com.bittorrent.client) or [Webtor.io](https://webtor.io) or use [seedr.cc](https://seedr.cc) to seeding torrent file.

## Write Ubuntu ISO to USB Drive:
- after sucessfully download `desktop-amd64.iso` file

- [Download](https://github.com/EtchDroid/EtchDroid/releases)  & [install](https://play.google.com/store/apps/details?id=eu.depau.etchdroid) EtchDroid on your Android device

- plug USB Drive into your mobile using OTG Cable
- Open EtchDroid > Write an image > chose downloaded `desktop-amd64.iso` from your device file manager Root/Download/desktop-amd64.iso > Grant access > OK > Write image > after sucessfully finish write `desktop-amd64.iso` file to USB Drive > Eject USB Drive from your device

## [Install Ubuntu desktop](https://ubuntu.com/tutorials/install-ubuntu-desktop#4-boot-from-usb-flash-drive):

- plug USB Drive into your computer USB Port and press restart button on your computer front panel > press F12 key on your cpmputer keyboard > select boot device as `UEFI: USB Drive` from your computer boot menu
- choose your language: English > Next > Next > Select your keyboard layout: English (US) > Next > connect to internet: based on on your case > Install Ubuntu > Next > How would you like to install Ubuntu?: Interactive installation > Next > What apps would you like to install to start with?: Default selection > Next > Install recommended proprietary software?: please check both box - `Install third-party software for graphics and Wi-Fi hardware` & `Download and install support for additional media formats` > Next > How do you want to install Ubuntu?: Erase disk and install Ubuntu > Next > Install now > Create your account - based on your personal details > Next > Select your timezone: pin your location on maps > Next > Install
- after `installation complete` click on `Restart now` > login to Ubuntu using your local account > finish.

- open Ubuntu Terminal and enter following commands:

~ `sudo apt update & sudo apt upgrade -y` 

> [`sudo`: its called super-user-do same as Windows Admin; `apt`: is Ubuntu package manager name; `update`: its update pakage on Ubuntu; `upgrade`: its update Ubuntu to latest versions; `-y`: its automatically accept all yes confermation dialog]

## Create Windows 11 Installation Media:

- go to [Download Windows 11](https://www.microsoft.com/en-us/software-download/windows11) website page > Download Windows 11 Disk Image (ISO) for x64 devices > Select Download: `Windows 11 (multi-edition ISO for x64 devices)` > Download Now > Select the product language: `English (United States)` > Confirm > Download - Windows 11 English: `64-bit Download`.

- install [WoeUSB-ng](https://github.com/WoeUSB/WoeUSB-ng) by running follwing commands in Ubuntu Terminal:

~ `sudo apt install git p7zip-full python3-pip python3-wxgtk4.0 grub2-common grub-pc-bin parted dosfstools ntfs-3g`

~ `sudo pip3 install WoeUSB-ng`

- open WoeUSB-ng from Ubuntu lanch pad > enter your Ubuntu local user password > Authenticate > From a disk image (iso): `Other Locations > Cpmputer / home / user_name / Download / Win11_English_x64.iso` > Open > Target device: `/dev/sda(USB Drive, GB)` > Install > Yes > installation succeeded! > OK

- Restart Ubuntu form Ubuntu power menu in controll centre > Restart > press F12 on your keyboard > select boot device: `UEFI: USB Drive, Partition 2 (USB Drive)` > Enter.

- Windows Setup - Language to install: English (United States) / Time and currency format: English (your_country) / keyboard or input method: English (your_country) > Next > Install now > Activate Windows: I don't have a product key > Windows 11 Pro > Next > Applicable notices and license terms: I accept the Microsoft Software License Terms. > Next > Which type of installation do you want?: Custom > select `Drive 0 Partition 3` > Delete > OK, select `Drive 0 Partition 2` > Delete > OK, select `Drive 0 Partition 1` > Delete > OK > Where do you want to install Windows?: select `Drive 0 Unallocated Space` > Next > Restart now.

- Is this the right  country or region?: your_country > Yes > Is this the right keyboard layout or input method?: US > Yes > Want to add a second keyboard layout?: Skip > make sure your computer connected to internet by LAN or USB Tethering, WiFi not work now since Windows does't comes with your computer motherboard wifi chip driver.
- Let's name your device: YourName's_Windows > Next > How would you like to set up this device?: Set up for personal use > Next > Unlock your Microsoft experience: Sign in > Let's add your Microsoft account: enter your Microsoft account credentials > Next > Welcome back, YourFirstName!: More options > Set up as a new PC > Are you sure?: Set up as a new PC > Create a PIN > Set up a PIN > OK > Choose privacy settings for your device: Location=Yes, Find my device=Yes, Diagonostic data=Yes, AllOthers=No > Accept > Let's customize your experience: Skip > Use your phone from your PC: Skip > Always have access to your recent browsing data: Not now > Enter your Windows local user PIN > Enter.

## Activation Windows 11 Pro for free also remove `Activate Windows` watermark form your screen permanently:

- Open PowerShell: To do that, right-click on the Windows start menu and select Terminal (Admin) > Yes
- Copy and paste the command below and press enter:
~ `irm https://get.activated.win | iex`
- from [Microsoft Activation Scripts](https://github.com/massgravel/Microsoft-Activation-Scripts):
- You will see the activation options. Choose `[1] HWID` for Windows activation.

## Activate Microsoft Office 365 for free:

- [Download](https://gravesoft.dev/office_c2r_links#english-en-us) Office > O365ProPlusRetail > Offline x86-x64 > Link
- Open File Explorer > Donloads / ProPlus2024Retail.iso > double click > Open > > Setup.exe > double click on it.


- Open PowerShell: To do that, right-click on the Windows start menu and select Terminal (Admin) > Yes 
- Copy and paste the command below and press enter:

  ~ `irm https://get.activated.win | iex`
- from [Microsoft Activation Scripts](https://github.com/massgravel/Microsoft-Activation-Scripts):
- You will see the activation options. Choose `[2] Ohook` for Office activation > `[1] Install Ohook Office Activation` > `[0] Exit`.

## Rcomended Apps:

AI

- [ChatGPT](https://github.com/lencx/ChatGPT/releases): get instant answers and inspiration
- [Google Gemini](https://github.com/nekupaw/gemini-desktop/releases): A simple Gemini desktop client (Minimize/Maximize:Ctrl+G;ChatUsingMicrophone:Ctrl+Shift+G)
- [Microsoft Copilot](https://www.microsoft.com/store/productId/9NHT9RB2F4HD?ocid=pdpshare): your everyday AI companion
  
Browser

- [Chrome](https://www.google.com/chrome/): Google Chromium
- [FireFox](https://www.mozilla.org/en-US/firefox/windows/): Firefox, is a free and open source web browser that puts your privacy first
- [Brave](https://brave.com/en-in/download/): Browser built with BAT based on Ether cryptocurrencies
- [Opera](https://www.opera.com/browsers/opera): Faster, safer and smarter than default browsers.
- [Bitwarden](https://github.com/bitwarden/clients/releases): open source cross platform password manager.

Cloud Drive

- [Google Drive](https://dl.google.com/drive-file-stream/GoogleDrive.exe): Google cloud storage.

Communication

- [Telegram](https://www.microsoft.com/store/productId/9NZTWSQNTD0S?ocid=pdpshare): cloud-based cross platfrom messaging app with a focus on security and speed
- [WhatsApp](https://www.microsoft.com/store/productId/9NKSQGP7F2NH?ocid=pdpshare): instant messaging service provide by Meta
- [Session Desktop](https://github.com/oxen-io/session-desktop/releases): open source cross platform Onion routing based messenger
- [Thunderbird](https://www.thunderbird.net/en-US/download/): free and open-source email client. + [uBlock Origin](https://addons.thunderbird.net/en-US/thunderbird/addon/ublock-origin/): Ads & Tracker Blocker + [Dark Reader](https://addons.thunderbird.net/en-us/thunderbird/addon/darkreader/): Dark mode for every email

Developer Tools

- [Git](https://gitforwindows.org/): Distributed revision control system
- [GitHub Desktop](https://desktop.github.com/download/) - Simple collaboration from your desktop.
- [Android Studio](https://developer.android.com/studio): official Integrated Development Environment (IDE) for Android app development.
- [android-platfrom-tool](https://developer.android.com/tools/releases/platform-tools): Google tool that allows you to use ADB commands for Android devices.
- [APKToolGUI](https://github.com/AndnixSH/APKToolGUI): Tool for reverse engineering 3rd party, closed, binary Android apps

Downloader

- [Winget](https://github.com/microsoft/winget-pkgs/tree/master/manifests): Another Package Manager for Windows.
  - Common winget commands:
    - Search for available apps: `winget search <app_name>`
    - Installs the specified app: `winget install <app_Id>`
    - Upgrades the specified app to the latest version:` winget upgrade <app_Id>` or `winget update <app_Id>`
    - Lists all installed apps: `winget list`
    - Uninstalls the specified app: `winget uninstall <app_Id>`
  - Example: To install the Visual Studio Code app using Winget, you would run: `winget install XP9KHM4BK9FZ7Q`

- [chocolatey](https://github.com/chocolatey/choco/releases) - other package manager for Windows
- [yt-dlp](https://github.com/microsoft/winget-pkgs/tree/master/manifests/y/yt-dlp/yt-dlp): command-line audio/video downloader
- [yt-dlp-gui](https://github.com/dsymbol/yt-dlp-gui): cross-platform GUI wrapper for yt-dlp

Education

- [mingw](https://code.visualstudio.com/docs/cpp/config-mingw): C++ Compiler
- [easyeda](https://easyeda.com/page/download): PCB design tool
- [kicad](https://www.kicad.org/download/windows/): Electronics design automation suite

Emulator

- [BlueStacks](): World's #1 Android Emulator.
- [WSL](https://www.microsoft.com/store/productId/9PDXGNCFSCZV?ocid=pdpshare): Run Linux Commands (bash) on Windows
- [Dolphin Emulator](https://dolphin-emu.org/download/): emulator for two recent Nintendo video game(GameCube and Wii) consoles

Entertainment

- [FreeTube](https://github.com/FreeTubeApp/FreeTube): feature-rich and user-friendly YouTube client with a focus on privacy.

Graphics & Design

- [Blender](https://www.blender.org/download/) - Blender is the free and open source 3D creation suite. It supports the entirety of the 3D pipeline: modeling, rigging, animation, simulation, rendering, compositing, motion tracking, and video editing.
- [Krita](https://krita.org/en/download/) - Krita is a cross-platform application for creating digital art files from scratch like illustrations, concept art, matte painting, textures, comics and animations.
- [Pencil2D Animation](https://github.com/pencil2d/pencil/releases) - Pencil2D is an animation/drawing software for macOS, Windows, and Linux. It lets you create traditional hand-drawn animation (cartoon) using both bitmap and vector graphics.
- [inkscape](https://inkscape.org/): free vector design tool
- [godot](https://github.com/godotengine/godot/releases): Multi-platform 2D and 3D game engine
- [Affinity Publisher](https://affinity.serif.com/en-gb/publisher/): next generation of professional page layout software.
- [OpenToonz](https://github.com/opentoonz/opentoonz/releases): Open-source 2D Animation Production Software

IDE

- [VS Code](https://code.visualstudio.com/): powerfull ide
- [vscodium](https://github.com/VSCodium/vscodium/releases): VS Code without MS branding/telemetry/licensing
- [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download/?section=windows): The IDE for Java and Kotlin enthusiasts.
- [MarkdownMonster](https://github.com/RickStrahl/MarkdownMonster/releases): An extensible Markdown Editor, Viewer for Windows.
- [MarkText](https://github.com/marktext/marktext/releases): A simple and elegant cross-platfrom markdown editor

Lifestyle

- [Sinric.Pro web](https://portal.sinric.pro/dashboard): simple way to connect your smart device to Google Home & it's free open source

Music

- [YouTube Music](https://github.com/th-ch/youtube-music): YouTube Music Desktop App bundled with custom plugins (and built-in ad blocker / downloader)
- [spotube](https://github.com/KRTirtho/spotube/releases): Open source Spotify client

Navigation

- [QGIS](https://qgis.org/download/): open source, cross platform geographical information system (GIS)

News

- [fluent-reader](https://github.com/yang991178/fluent-reader/releases): Modern desktop RSS reader built with Electron + https://9to5google.com/feed/

Notes

- [notesnook](https://github.com/streetwriters/notesnook/releases): open source & cross platform end-to-end encrypted note taking alternative to Evernote.
- [keep](https://github.com/andrepolischuk/keep/releases): Desktop app for Google Keep Notes packaged with Electron
- [Standard Notes](https://github.com/standardnotes/app/releases/latest) : end-to-end encryption sync cross platform notes taking apps

Personalisation

- [OpenRGB](https://gitlab.com/CalcProgrammer1/OpenRGB/-/releases/) Open source RGB lighting control software.
- [Windows Auto Dark Mode](https://github.com/AutoDarkMode/Windows-Auto-Night-Mode/releases): Automatically switches between the dark and light theme
- [Monitorian](https://www.microsoft.com/store/productId/9NW33J738BL0?ocid=pdpshare): adjust the brightness of monitors using monitor Display Data Channel/Command Interface(DDC/CI) controller over VGA/HDMI/DP/Type-C.

Photo & Video

- [DavinchiResolve](https://www.blackmagicdesign.com/products/davinciresolve): Professional video editing tools, Alternative to Adobe Premiere Pro
- [Microsoft Clipchamp](https://www.microsoft.com/store/productId/9P1J8S7CCWWT?ocid=pdpshare): Create videos with a few clicks in Clipchamp, the easy video editor by Microsoft.
- [Jitsi Meet Electron](https://github.com/jitsi/jitsi-meet-electron/releases): Jitsi Meet desktop application powered by React native
- [Ente Photos](https://github.com/ente-io/photos-desktop): open source cross platform end-to-end encryption sync Photos app Alternative to Google Photos & Apple Photos.
- [GIMP](https://www.gimp.org/downloads/): Free & Open Source Image Editor
- [darktable](https://github.com/darktable-org/darktable/releases): free Adobe Lightroom Classic replacement.

Player

- [VLC](https://apps.microsoft.com/store/detail/XPDM1ZW6815MQM?ocid=pdpshare): free and open source cross-platform multimedia player

Productivity

- [Microsoft Office 365](https://github.com/arghya339/some-stupid-thing/blob/main/Install%20Windows/Install-Windows-Linux-using-Android.md#activate-microsoft-office-365-for-free)
- [LibreOffice](https://www.libreoffice.org/download/download-libreoffice/?type=windows-x86_64): free and powerful office suite, Alternative to Microsoft Office
- [Google-Assistant-Unofficial-Desktop-Client](https://github.com/Melvin-Abraham/Google-Assistant-Unofficial-Desktop-Client/releases): cross-platform unofficial Google Assistant Client for Desktop

Security

- [VirusTotal](https://docs.virustotal.com/docs/desktop-apps#windows-uploader): Drag and drop files scan
- [Avast antivirus](https://www.avast.com/en-in/index#pc): best free antivirus for Windows
- [Cryptomator](https://cryptomator.org/downloads/): Multi-platform transparent client-side encryption of your files in the cloud
- [EnteAuth](https://github.com/ente-io/ente/releases?q=auth&expanded=true): Open Source Authenticator with cross platform end-to-end encryption data sync.

Sharing Files

- [LocalSend](https://github.com/microsoft/winget-pkgs/tree/master/manifests/l/LocalSend/LocalSend): free, open-source, cross-platform file sharing tool that allows you to share files to nearby devices.

Social Networking

- [Vencord](https://github.com/Vencord/Installer/releases): Discord Desktop client mod
- [BetterDiscord](https://github.com/BetterDiscord/Installer/releases): enhances Discord desktop app with new features.

Streaming

- [OBS Studio](https://obsproject.com/download): free and open source software for video recording and live streaming. + [DroidCam OBS Plugins](https://droidcam.app/obs/#): connect your phone and get high quality audio & video directly into OBS Studio, just like a regular camera
- [IriunWebcam](https://iriun.com/) : use your Android phone as a wireless webcam
- [QtScrcpy](https://github.com/barry-ran/QtScrcpy/releases): Displaying and controlling Android devices via USB or over Local network.
- [ChromeRemoteDesktop](https://remotedesktop.google.com/access): control your Windows from another device (phone/computer)

Tools

- [pot-desktop](https://github.com/pot-app/pot-desktop/releases): cross-platform software for text translation and recognition.

Utilities

- [Rufus](https://github.com/pbatard/rufus/releases): Reliable USB Formatting Utility
- [Balena Etcher](https://github.com/balena-io/etcher) - Flash OS images to SD cards & USB drives, safely and easily.
- [WinRAR](https://www.win-rar.com/predownload.html?&L=0): The Windows file archiver (zip,rar,7z)
- [HandBrake](https://github.com/HandBrake/HandBrake/releases) : video transcoder (mkv/mp4)

VPN & Proxy

- [DNS Changer](https://github.com/DnsChanger/dnsChanger-desktop/releases): DNS Changer
- [Cloudflare WARP](https://1.1.1.1/): makes your Internet more private
- [WireGuard](https://wireguard.com/install/): WireGuard is a fast, modern, and secure VPN tunnel. + [WireGuard Config by ProtonVPN](https://account.protonvpn.com/downloads): free, secure, and ultra-fast VPN designed to protect your privacy online and to unblock access to popular websites and streaming platforms, no matter where you are. Free VPN features | No ads | No logs | Unlimited and free forever | Strongest protocols (Wireguard, Stealth) | Open source & Ads and malware blocker (Netshield).
- [AdGuard VPN](https://adguard-vpn.com/en/windows/overview.html): AdGuard VPN for Windows
- [Tor Browser](https://www.torproject.org/download/): Tor-powered Browser

## Releted Repo:

- [AlderLake RaptorLake OpenCore Install Guide](https://github.com/arghya339/some-stupid-thing/blob/main/AlderLake-RaptorLake-OpenCore-Install-Guide.md)

## Support

- Donation: [PayPal/@arghyadeep339](https://www.paypal.com/paypalme/arghyadeep339)
- Subscribe: [YouTube/@MrPalash360](https://www.youtube.com/channel/UC_OnjACMLvOR9SXjDdp2Pgg/videos?sub_confirmation=1)
- Follow: [Telegram](https://t.me/MrPalash360)
- Join: [Telegram](https://t.me/MrPalash360Discussion)
