## Configuration

| Model     | XPS15-7590 / MacBookPro16,1    | Version        | Ventura 13.5 / OpenCore 0.9.3 |
| :-------- | :----------------------------- | :------------- | :---------------------------- |
| Processor | Intel Core i7-9750H            | Graphics       | Intel UHD Graphics 630        |
| Memory    | Crucial DDR4 2666MHz 16GB x 2  | Storage        | WD BLACK SN850 NVMe SSD 2T    |
| Audio     | Realtek ALC298                 | WiFi/Bluetooth | Dell Wireless 1830            |
| Display   | Sharp SHP14BA (MWP1T-LQ156M1) <br> 15.6-inch WLED FHD non-touchscreen | Monitor | No |

### Not Working

- DiscreteGPU
- Thunderbolt
- Fingerprint

## Pre Installation

### OpenCore Configurator

You can use [*OCAuxiliaryTools*](https://github.com/ic005k/OCAuxiliaryTools), a Cross-platform GUI management tool for OpenCore.

### BIOS

- BIOS version: 1.21.0
- SATA Mode: AHCI

### UEFI changes

- From Opencore boot screen long press the SPACE bar, go to modGRUBShell and set the values for CFG unlock, DVMT Pre-Allocated, DVMT Total Gfx Mem and overclocking lock to the following:
  
```sh
setup_var_cv Setup 0x6ED 0x01 0x00
setup_var 0xA10 0x02
setup_var 0xA11 0x03
setup_var_3 0x789 0x00
```

## Installation

**Please use [the latest release](https://github.com/jackhanyuan/Dell-XPS15-7590-Hackintosh/releases/latest).**

### UHD Display

If your laptop display is 4k, you have to modify your config.plist:

- Find `dpcd-max-link-rate` and change its value to `FAAAAA==`

## Post Installation

### Sleep Wake

Please run following commands:

```shell
sudo pmset -a hibernatemode 0
sudo pmset -a autopoweroff 0
sudo pmset -a standby 0
sudo pmset -a proximitywake 0
```

### Network Interface

Please open `System Report-Network-Wi-Fi` and check your network interface, if not **en0**, you have to:

1. delete all items in `system preferences-network` left side list.
2. remove `/Library/Preferences/SystemConfiguration/NetworkInterfaces.plist`
3. reboot your computer
4. enter `system preferences-network`, click '+' and add Wi-Fi back.

### SN MLB SmUUID and ROM

You can use [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools) (PI -> Generic) to generate SN, MLB and SmUUID.

#### SmUUID

Highly recommend you to use  **Windows system UUID** as SmUUID: run  `wmic csproduct get UUID` in Windows CMD.

#### ROM

Highly recommend you to use the **MAC address of en0** as ROM: run  `ifconfig en0 | awk '/ether/{print $2}' | sed -e 's/\://g'` in Mac Terminal.

### Font Smoothing

If you are using FHD(1080p) display, you may want to enable font smoothing:

```sh
defaults write -g CGFontRenderingFontSmoothingDisabled -bool NO # YES to disable
```

## Credits

- [xxxzc](https://github.com/xxxzc) - Reference [xps15-9570-macos](https://github.com/xxxzc/xps15-9570-macos) for most of the config.
- [acidanthera](https://github.com/acidanthera) - Almost all kexts and drivers.
- [dortania](https://github.com/dortania/OpenCore-Install-Guide) - OpenCore Install Guide.
- [daliansky](https://github.com/daliansky) - Hackintosh EFI and installation tutorial.
- [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) - OpenCore bootloader.
- [OCAT](https://github.com/ic005k/OCAuxiliaryTools) - OCAuxiliaryTools.
- [Hackintool](https://github.com/headkaze/Hackintool) - The Swiss army knife of vanilla Hackintoshing.
- [one-key-hidpi](https://github.com/xzhih/one-key-hidpi) - Enable macOS HiDPI.
