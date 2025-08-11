# How to setup everything to get 60 fps in games
In this guide you will learn how to setup EOS and how to use FPS Locker to achieve 60 fps.
## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Fixing archive bit](#fixing-archive-bit)
- [Setting up the kip](#setting-up-the-kip)
- [Turning on the overclock using sys-clk](#turning-on-the-overclock-using-sys-clk)
- [Using FPSLocker to Unlock 60 FPS](#using-fpslocker-to-unlock-60-fps)
- [Using ReverseNX-RT](#using-reversenx-rt)
- [Using Status Monitor to monitor the FPS](#using-status-monitor-to-monitor-the-fps)
- [Using EdiZon](#using-edizon)
- [Troubleshooting and Further Information](#troubleshooting-and-further-information)
- [Credits](#credits)
- [Mariko(Oled, Lite, V2) settings guide](https://rentry.co/mariko)
- [Erista(V1) settings guide](https://rentry.co/erista)
- [How to test stability](https://rentry.co/howtoteststability)

### Prerequisites

- **Latest [Atmosphere CFW](https://github.com/Atmosphere-NX/Atmosphere/releases):** Ensure you have latest Atmosphere CFW installed. Other CFWs like SX OS are not supported.
- **USB Transfer Tool:** Use Atmosphere's USB Transfer Tool homebrew for file transfers. If using Hekate's USB Mass Storage on non-Windows OS, run Hekate's Archive Bit Fixer after transferring all files.

### Installation

1. **SaltyNX **
    - Download the latest `SaltyNX` release from [this link](https://github.com/masagrator/SaltyNX/releases/latest).
    - Unpack the zip file.
    - Copy the `SaltySD` and `atmosphere` folders to the root of your SD card.
    - Accept any prompts about overwriting folders.

2. **nx-ovlloader+**
    - Download the latest `nx-ovlloader+` release from [this link](https://github.com/ppkantorski/nx-ovlloader/releases).
    - Extract  `nx-ovlloader+.zip` .
    - Copy the `atmosphere` folder to the root of your SD card.
    - Accept any prompts about overwriting folders.

3. **EOS**
    - Download the latest `EOS` version from [this link](https://github.com/halop/OC-Switchcraft-EOS/releases/latest)
    - Extract the archive.
    - Open the `copy_to_SD` folder.
    - Copy its contents to the root of your SD card.
    - Accept any prompts about overwriting folders.

4. **Status Monitor Overlay with real voltages**
    - Download the `Status Monitor Overlay` with real voltages from [this link](https://github.com/CatcherITGF/NX-Venom/raw/main/Sources/NXVenom/switch/.overlays/Status-Monitor-Overlay.ovl).
    - Copy the `Status-Monitor-Overlay.ovl` file to the `switch\.overlays` folder.
    - Note: It may not be visible in USB Mass Storage, but it’s there.
    - Accept any prompts about overwriting folders.


5. **FPSLocker**
    - Download the `FPSLocker` release from [this link](https://github.com/masagrator/FPSLocker/releases/latest).
    - Copy the `FPSLocker.ovl` file to the `switch\.overlays` folder.
    - Note: It may not be visible in USB Mass Storage, but it’s there.

6. **Ultrahand**
    - Download the latest `Ultrahand` release from [this link](https://github.com/ppkantorski/Ultrahand-Overlay/releases/latest).
    - Copy the `ovlmenu.ovl` file to the `switch\.overlays` folder.
    - Note: It may not be visible in USB Mass Storage, but it’s there.
	- Accept any prompts about overwriting folders.

7. **ReverseNX-RT**
    - Download the latest `ReverseNX-RT` release from [this link](https://github.com/masagrator/ReverseNX-RT/releases/latest).
    - Copy the `ReverseNX-RT-ovl.ovl` file to the `switch\.overlays` folder.
    - Note: It may not be visible in USB Mass Storage, but it’s there.
    - Download the latest `ReverseNX-Tool` release from [this link](https://github.com/masagrator/ReverseNX-Tool/releases/latest).
    - Copy the `ReverseNX-Tool.nro` file to the `switch` folder.

8. **hekate-ipl**
    - Open the `bootloader/hekate_ipl.ini` file on your SD card.
    - Add the following line to your boot entry: `kip1=atmosphere/kips/*`.

 Alternatively, you can replace the content of your `hekate_ipl.ini` file with the following content:

```ini
{------ Atmosphere ------}
[CFW on EMUNAND]
fss0=atmosphere/package3
kip1patch=nosigchk
kip1=atmosphere/kips/*
cal0blank=1
emummcforce=1

{------ Atmosphere ------}
[CFW on SYSNAND]
fss0=atmosphere/package3
kip1patch=nosigchk
kip1=atmosphere/kips/*
cal0blank=0
emummc_force_disable=1

{------ Atmosphere ------}
[CFW on EMUNAND without KIP]
fss0=atmosphere/package3
kip1patch=nosigchk
cal0blank=1
emummcforce=1

{------ Atmosphere ------}
[CFW on SYSNAND without KIP]
fss0=atmosphere/package3
kip1patch=nosigchk
cal0blank=0
emummc_force_disable=1
```

9. (Optional) **EdiZon Overlay**
   - Download the latest `ovlEdiZon.ovl` release from [this link](https://github.com/ppkantorski/EdiZon-Overlay/releases/latest)
   - Copy the `ovlEdiZon.ovl` file to the `switch\.overlays` folder.
   - Note: It may not be visible in USB Mass Storage, but it’s there.
   - Navigate to the `atmosphere/config_templates` folder on the root of your microSD card.
   - Open the `system_settings.ini` file and paste this at the bottom of all the text:

```ini
[atmosphere]
; Controls whether dmnt cheats should be toggled on or off by
; default. 1 = toggled on by default, 0 = toggled off by default.
dmnt_cheats_enabled_by_default = u8!0x0
; Controls whether dmnt should always save cheat toggle state
; for restoration on new game launch. 1 = always save toggles,
; 0 = only save toggles if toggle file exists.
dmnt_always_save_cheat_toggles = u8!0x1
```

- Move the `system_settings.ini` file from the `atmosphere/config_templates` folder to the `atmosphere/config` folder.


###Fixing archive bit
- Boot `Hekate`, select `Tools` > `Arch Bit • RCM • Touch • pkg1/2`> `Fix Archive Bit`.

### Setting up the kip

0. **Check HW and Fuses:**
	- Boot `Hekate`.
	- Go to Console Info - HW & Fuses.
	- Note your DRAM ID, CPU Speedo 0, CPU Speedo 2, and SoC Speedo.

1. **Launch CFW:**
    - Launch CFW on your switch.

2. **Accessing Overlays:**
    - Press `ZL`, `ZR`, and `DPAD DOWN` simultaneously to access overlays. If that doesn't work, try `L`, `D-pad down` and `R-stick`.
    - To edit the key combination in `Ultrahand`, press `+` then navigate into `Key Combo` menu. I personally use `L`, `R`, and `DPAD UP`.

3. **Open OC Switchcraft EOS Overlay:**
	- Open `Ultrahand`
	- Press `D-pad right` and click on `OC Switchcraft EOS`
- In case this doesn't appear, fix [archive bit](#fixing-archive-bit)
4. **Tweak the settings of the KIP inside OC Switchcraft EOS Overlay:**
	- Follow those guides based on your configuration to do proper overclocking.

!!!note You have to restart the console every time you edit something in the kip settings to apply new settings.

- [Mariko(Oled, Lite, V2) settings guide](https://rentry.co/mariko)

- [Erista(V1) settings guide](https://rentry.co/erista)

!!!danger If you see any RAM artifacts, hold the power button until it shuts down to avoid corruption. Lower some timings.

After you setup the kip, follow this guide to check stability:
- [How to test stability](https://rentry.co/howtoteststability)

###Turning on the overclock using sys-clk

- Open `Ultrahand` and select `sys-clk`.
- Enable `sys-clk` and adjust the settings by pressing on `Edit app profile` or `Edit global profile` for desired performance.
- It's recommended to set the maximum RAM setting in the global profile override for significant performance gains without substantial power draw. Ensure to test RAM stability first (refer to the settings guide for instructions).

Miscellaneous Settings:
- `Uncapped GPU Clocks`: Removes GPU clock cappings	. Turn this ON.
- `Override Boost Mode`: Overrides official boost mode with user set profile clocks. Turn this OFF.
- `Auto CPU Boost`: Sets cpu clock to boost clock when core#3 load ≥ 90%. Turn this ON.
- `Sync ReverseNX`: Overrides profile to match reversenx state. Turn this OFF.

### Using FPSLocker to Unlock 60 FPS

- Launch a game and open `Ultrahand`. Select `FPSLocker`.
- Click the `Increase FPS target` button six times. The custom FPS target should be set to 60.
- If the FPS does not increase past 30, the game may require a patch:
   - Open `Ultrahand`, click on `FPSLocker`, then go to `Advanced Settings`.
   - Select `Check/download config file`, wait for it to complete, then choose `Convert config to patch`.
   - Restart the game and set the FPS target to 60 in `FPSLocker`.
- If a patch isn't available:
   - Open `Ultrahand`, click on `FPSLocker`, then go to `Advanced Settings`.
   - Select `Window Sync` and set it to `semi`.
- Visit the [FPSLocker Warehouse](https://github.com/masagrator/FPSLocker-Warehouse) to download the latest set of patches for games requiring further tweaks to achieve a proper FPS boost.

!!! note **Note:** Some games may require additional 60 FPS mods or cheats.
### Using ReverseNX-RT

1. Launch a game and open `Ultrahand`. Select `ReverseNX-RT`.
2. Press the `Change System Control` button so the mode won't be controlled by the system anymore.
3. Press the `Change Mode` button to set it to the desired mode.

!!! danger **Warning:** Never use docked mode while unplugged if `Sync ReverseNX` is enabled in `sys-clk`. This will set the clocks to docked mode and may cause battery damage.

### Using Status Monitor to monitor the FPS

1. Launch a game and open `Ultrahand`. Select `Status Monitor`.
2. Choose a mode to check FPS, temperature, voltage, usage, etc. It's recommended to use `Mini` or `Micro mode`.
3. To exit the overlay, hold your `Ultrahand` key combo for 3 seconds.

###Using EdiZon
0. Download cheats. Launch `All-in-One Switch Updater` from the `hbmenu`. Move to `Download cheats` on the left panel, then select `Download GBAtemp.net cheat archive (ver xxxxxxxx)` from the right panel (this will only download cheats for the titles you have installed. If you want to download all available cheats you can select `Download GBAtemp.net cheat codes`).
1. Launch a game and open `Ultrahand`. Select `EdiZon`. Click on `Cheats`.
2. Enable and disable cheats by pressing A, a cheat is enabled if it says 'On'. Sometimes cheats may require turning them on and off for them to work. Ensure you disable cheats you are not using i.e. disable the 30FPS cheat if using the 60FPS cheat or disable the 720p cheat if using a 1080p cheat.

### Troubleshooting and Further Information

- **READMEs:** For any questions or troubleshooting, refer to the READMEs of the respective tools.
- **Community Support:** Engage with the community on forums and Discord for additional support and updates.

**My Switch won't boot after I have installed SWITCHCRAFT:**

- Your atmosphere version is likely not up-to-date, update your atmosphere version.
- CPU UV level is too high, lower it or set it to 0.
###Credits



- This guide is a modified version of this [gist](https://gist.github.com/masagrator/65fcbd5ad09243399268d145aaab899b) created by masagrator.
- Some parts from this guide were adapted from ChanseyIsTheBest's guides
