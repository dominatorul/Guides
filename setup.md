# 🎮 How to Set Up Everything for **60 FPS** in Games! 🎮

Welcome! In this guide, you’ll set up **EOS** and **FPS Locker** to boost performance to 60 FPS. This guide is packed with steps and tips to make the whole process easier. Let’s dive in! 🕹️

---

## 📋 Table of Contents
- [🎬 Before You Start](#before-you-start)
- [💾 Installation](#installation)
- [🛠 Fixing Archive Bit](#fixing-archive-bit)
- [⚙️ Setting Up the KIP](#setting-up-the-kip)
- [🚀 Enabling Overclock with sys-clk](#enabling-overclock-with-sys-clk)
- [🔓 Unlocking 60 FPS with FPSLocker](#Unlocking-60-fps-with-fpslocker)
- [💡 Using ReverseNX-RT](#using-reversenx-rt)
- [📊 Monitoring FPS with Status Monitor](#using-status-monitor-to-monitor-the-fps)
- [🎚 Using EdiZon](#using-edizon)
- [⚠️ Troubleshooting and Further Information](#troubleshooting-and-further-information)
- [🙏 Credits](#credits)
- **Extra Settings**  
   - [Mariko (Oled, Lite, V2) Guide](https://rentry.co/mariko)  
   - [Erista (V1) Guide](https://rentry.co/erista)  
   - [Testing Stability](https://rentry.co/howtoteststability)

---

### 🎬 Before You Start

🛠**Install the latest versions** of the following essential tools:

- **[Atmosphere](https://github.com/Atmosphere-NX/Atmosphere/releases/)** - the custom firmware you’ll be using.  
- **[Hekate](https://github.com/CTCaer/hekate/releases/latest)** - includes USB Mass Storage (UMS) mode.


🛠 **Back Up eMMC using Hekate**

1. Open `Hekate` and navigate to the `Tools` section, then select `Backup eMMC`.
2. Create a backup of `eMMC BOOT0 & BOOT1`.
3. Back up the `eMMC RAW GPP` partition.

🛠 **Back Up emuMMC using Hekate**

1. Open `Hekate` and navigate to the `Tools` section, then select `Backup eMMC`.
2. To back up `emuMMC`, enable the option for `SD emuMMC Raw Partition` .
3. Create a backup of `SD emuMMC BOOT0 & BOOT1`.
4. Back up the `SD emuMMC RAW GPP` partition.

A `backup` folder will now be created in the root of your SD card. Copy the folder to your PC for safekeeping, then delete it from the root of your microSD card to free up space. Be sure to store the folder safely.

!!!note Remember to [**fix the archive bit**](#fixing-archive-bit) after using UMS.

---

### 💾 Installation

Follow these steps to download and install the necessary tools on your SD card:

1. **SaltyNX**
   - 📥 Download from [this link](https://github.com/masagrator/SaltyNX/releases/latest).
   - Unpack the ZIP file.
   - Copy the `SaltySD` and `atmosphere` folders to the root of your SD card.

2. **nx-ovlloader+**
   - 📥 Download from [this link](https://github.com/ppkantorski/nx-ovlloader/releases).
   - Copy the `atmosphere` folder to the root of your SD card.

3. **EOS** 
   - 📥 Download from [this link](https://github.com/halop/OC-Switchcraft-EOS/releases/latest).
    - Open the `copy_to_SD` folder.
    - Copy its contents to the root of your SD card.

4. **Status Monitor Overlay with real voltages**
   - 📥 Download from [this link](https://github.com/CatcherITGF/NX-Venom/raw/main/Sources/NXVenom/switch/.overlays/Status-Monitor-Overlay.ovl).
   - Place `Status-Monitor-Overlay.ovl` in `switch/.overlays`.

5. **FPSLocker**
   - 📥 Download from [this link](https://github.com/masagrator/FPSLocker/releases/latest).
   - Copy `FPSLocker.ovl` to `switch/.overlays`.

6. **Ultrahand**
   - 📥 Download from [this link](https://github.com/ppkantorski/Ultrahand-Overlay/releases/latest).
   - Place `ovlmenu.ovl` in `switch/.overlays`.

7. **ReverseNX-RT**
   - 📥 Download from [this link](https://github.com/masagrator/ReverseNX-RT/releases/latest).
   - Place `ReverseNX-RT-ovl.ovl` in `switch/.overlays`.

8. **hekate-ipl**
   - Add the line `kip1=atmosphere/kips/*` to to your boot entry from `bootloader/hekate_ipl.ini` file on your SD card.

!!!note If you’re unfamiliar with how to edit the `hekate_ipl.ini`, you can download a [sample file](https://github.com/user-attachments/files/17683638/copy_to_SD.zip), open the `copy_to_SD` folder and copy its contents to the root of your SD card ***Note: This will override your current launch menu.***

9. **(Optional) EdiZon Overlay**
   - 📥 Download from [this link](https://github.com/ppkantorski/EdiZon-Overlay/releases/latest).
   - Copy the `ovlEdiZon.ovl` file to the `switch/.overlays` folder.
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
10. **(Optional) NX-FanControl**

   - 📥 Download from [this link](https://github.com/Zathawo/NX-FanControl/releases/latest)
   - Copy the `atmosphere` and `switch` folders to the root of your SD card.

---

### 🛠 Fixing Archive Bit

After booting Hekate, navigate to **Tools** > **Arch Bit • RCM • Touch • pkg1/2** > **Fix Archive Bit**. This ensures the files can be read properly.

---

### ⚙️ Setting Up the KIP

0. **Check Console Info**  
   - Boot into Hekate, and go to Console Info - HW & Fuses. Record the **DRAM ID, CPU Speedo 0, CPU Speedo 2,** and **SoC Speedo.**

1. **Launch CFW**  
   - Launch the custom firmware (CFW) on your console.

2. **Accessing Overlays:**
    - Press `ZL`, `ZR`, and `DPAD DOWN` simultaneously to access overlays. If that doesn't work, try `L`, `D-pad down` and `R-stick`.
    - To edit the key combination in `Ultrahand`, press `+` then navigate into `Key Combo` menu. I personally use `L`, `R`, and `DPAD UP`.

3. **Open OC Switchcraft EOS Overlay:**
	- Open `Ultrahand`
	- Press `D-pad right` and click on `OC Switchcraft EOS`
- In case this doesn't appear, fix [archive bit](#fixing-archive-bit)

4. **Adjust KIP Settings**  
   - Use the appropriate settings based on your console configuration:
     - [Mariko (Oled, Lite, V2) Guide](https://rentry.co/mariko)
     - [Erista (V1) Guide](https://rentry.co/erista)
   
!!!note Restart your console after changing KIP settings to apply them.

!!!danger If you notice RAM artifacts, hold down the power button to shut down and prevent corruption, then reduce some timings.

Check your settings’ stability here: [How to test stability](https://rentry.co/howtoteststability)

---

### 🚀 Enabling Overclock with sys-clk
- Open `Ultrahand` and select `sys-clk`.
- Enable `sys-clk` and adjust the settings by pressing on `Edit app profile` or `Edit global profile` for desired performance.
- It's recommended to set the maximum RAM setting in the global profile override for significant performance gains without substantial power draw. Ensure to test RAM stability first (refer to the settings guide for instructions).
  
Miscellaneous Settings:
- `Uncapped GPU Clocks`: Removes GPU clock cappings	. Turn this ON.
- `Override Boost Mode`: Overrides official boost mode with user set profile clocks. Turn this OFF.
- `Auto CPU Boost`: Sets cpu clock to boost clock when core#3 load ≥ 90%. Turn this ON.
- `Sync ReverseNX`: Overrides profile to match reversenx state. Turn this OFF.

---

### 🔓 Unlocking 60 FPS with FPSLocker

- Launch a game and open `Ultrahand`. Select `FPSLocker`.
- Click the `Increase FPS target` button six times. The custom FPS target should be set to 60.
- If the FPS does not increase past 30, the game may require a patch:
   - Open `Ultrahand`, click on `FPSLocker`, then go to `Advanced Settings`.
   - Select `Check/download config file`, wait for it to complete, then choose `Convert config to patch`.
   - Restart the game and set the FPS target to 60 in `FPSLocker`.
- If a patch isn't available:
   - Open `Ultrahand`, click on `FPSLocker`, then go to `Advanced Settings`.
   - Select `Window Sync` and set it to `semi`.
Visit the [FPSLocker Warehouse](https://github.com/masagrator/FPSLocker-Warehouse) to download patches for games needing further tweaks.

!!!note Some games may require 60 FPS mods or cheats in addition to FPSLocker.

---

### 💡 Using ReverseNX-RT

1. Launch a game and open `Ultrahand`. Select `ReverseNX-RT`.
2. Press the `Change System Control` button so the mode won't be controlled by the system anymore.
3. Press the `Change Mode` button to set it to the desired mode.

!!!danger **Warning:** Never use docked mode when unplugged if `Sync ReverseNX` is enabled in sys-clk. This will set the clocks to docked mode and may damage the battery.

---

### 📊 Monitoring FPS with Status Monitor

1. Launch a game and open `Ultrahand`. Select `Status Monitor`.
2. Choose a mode to check FPS, temperature, voltage, usage, etc. It's recommended to use `Mini` or `Micro mode`.
3. To exit the overlay, hold your `Ultrahand` key combo for 3 seconds.

---

### 🎚 Using EdiZon

0. Download cheats. Launch `All-in-One Switch Updater` from the `hbmenu`. Move to `Download cheats` on the left panel, then select `Download GBAtemp.net cheat archive (ver xxxxxxxx)` from the right panel (this will only download cheats for the titles you have installed. If you want to download all available cheats you can select `Download GBAtemp.net cheat codes`).
1. Launch a game and open `Ultrahand`. Select `EdiZon`. Click on `Cheats`. 
2. Enable and disable cheats by pressing A, a cheat is enabled if it says 'On'. Sometimes cheats may require turning them on and off for them to work. Ensure you disable cheats you are not using i.e. disable the 30FPS cheat if using the 60FPS cheat or disable the 720p cheat if using a 1080p cheat.

---

### ⚠️ Troubleshooting and Further Information

- **READMEs:** Check each tool's README for in-depth guidance.
- **Community Support:** Seek help from forums and Discord for updates.

❌ **Console not booting?**

Update Atmosphere or set CPU UV level to 0.

### 🙏 Credits

This guide is adapted from masagrator's [original gist](https://gist.github.com/masagrator/65fcbd5ad09243399268d145aaab899b) with contributions from ChanseyIsTheBest.

Happy gaming! 🚀
