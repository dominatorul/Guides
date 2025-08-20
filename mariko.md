# Mariko OC Guide

*Made with love by Dominatorul. Some parts of this guide belong to ChanseyIsTheBest.*

---

## Table of Contents
- [Safety Disclaimer](#safety-disclaimer)
- [Mariko Limits](#mariko-limits)
- [Monitoring Your Switch](#monitoring-your-switch)
- [Checking Speedo and RAM Type](#checking-speedo-and-ram-type)
- [RAM Tiers](#ram-tiers-higher-is-better)
- [OC Settings for Switchcraft](#oc-settings-for-switchcraft)
   - [CPU Settings](#cpu-settings)
   - [GPU Settings](#gpu-settings)
   - [RAM Settings](#ram-settings)
- [Clock Settings](#clock-settings)
   - [Mariko Max Safe on Battery](#mariko-max-safe-on-battery-hac-001-01-heg-001)
   - [Switch Lite Max Safe Clocks on Battery](#switch-lite-max-safe-clocks-on-battery-hdh-001)
   - [Mariko Max Clocks Docked and Plugged](#mariko-max-clocks-docked-and-plugged-hac-001-01-heg-001)
   - [Switch Lite Max Clocks Plugged](#switch-lite-max-clocks-plugged-hdh-001)
- [Troubleshooting](#troubleshooting)
- [How to test stability](https://rentry.co/howtoteststability)

---

# Safety Disclaimer
!!! info ** Overclocking is inherently risky as it pushes the system beyond its original design. The risk level depends on how much you overclock and whether you stay within the limits of the chip and hardware.**

!!! danger **Unstable RAM overclocking can cause SYSNAND/EMUNAND corruption and SD card corruption, particularly if done on SYSNAND. Test the overclock settings on EMUNAND and back it up before installing Switchcraft.**

---

# Mariko Limits

### Mariko CPU Limits:
- 5A limit reached at 2397MHz (CPU UV1) or 2295MHz (< 1650 CPU speedo).
- Use higher UV levels to avoid exceeding the PMIC limit.

### Mariko GPU Limits:
- 10A limit reached at 1228MHz (GPU UV1) with moderate speedos (1650).
- Disabling GPU scheduling overloads the PMIC, potentially causing damage.

### Charger IC Limit:
- 18W limit restricts overclocking for both Erista and Mariko units (12W on Switch Lite). This is the main limiting factor, but the PMIC current limits for CPU and GPU will be reached first.

### GPU Scheduling

This setting adjusts how much of your GPU can be utilized:

- **On:** Limits GPU usage to ~96.7%
- **Off:** Limits GPU usage to ~99.7% (up to ~5% performance boost)
- **Recommended:** GPU scheduling **off**.
!!! danger  ** Warning:** Disabling GPU Scheduling will slightly increase power draw. Use it with caution.

---

# Monitoring Your Switch
- Use status monitor overlay to indicate if you've bypassed the charger IC limit (e.g., -1W displayed while charging).
- To get the best results, be sure your battery is 10-90% to display the real charging

---

# Checking Speedo and RAM Type

1. Boot Hekate.
2. Go to Console Info > HW & Fuses.
3. Note your DRAM ID, CPU Speedo 0, CPU Speedo 2, and SoC Speedo.
   - Speedos typically range from 1450 to 1810. A higher speedo means less voltage is needed for the same clock speed. A speedo of 1650 is generally considered good.

**Speedo Brackets**
>  - Speedos are divided into **brackets**.  
>  - **CPU UV mode** depends on the position within your bracket, but the resulting **voltage** depends on your specific speedo.
>  - It doesn’t matter how high you can set CPU UV mode — what matters is using your **maximum possible** CPU UV mode.

---

#  RAM Tiers (Higher is better)

| Tier        | RAM ID           |
|-------------|------------------|
| GOD-tier    | NEI/NEE, WT:B          |
| S-tier      | AA-MGCR, AA-MGCL |
| A-tier      | WT:F             |
| B-tier      | AM-MGCJ, WT:E    |
| C-tier      | AB-MGCL     |
| D-tier      | NME     |

---

# OC Settings for Switchcraft

## CPU Setting

- **Boost Clock**
  - **2397 MHz:** For Speedo <1600
  - **2499 MHz:** For Speedo >1600
  - **2601 MHz:** For Speedo >1650

- **Undervolt Mode:** 1–8 (start with 4).
  - Increase gradually if stable and find your highest stable value.
  - If the console fails to boot, lower the value.

- **High Freq UV:** 5–10 (find your highest stable value).
  - A few rare units may reach 11–12 — test carefully.

- **Low Freq Vmin:** 590 mV

- **High Freq Vmin:** 720–750 mV
  - Test lower values if your CPU bin is strong.

- **Voltage Limit:**
  - **1120 mV:** Safe
  - **1160 mV:** Use with caution

- **Table Config:** AUTO

> **ℹ️ Note:** Exceeding the PMIC limit during **Boost Mode** is safe, as it only occurs for short bursts (typically under 30 seconds), preventing long-term hardware stress.


## GPU Settings

- **Undervolt Mode:** 2

- **DVFS:**
  - **2 (Hijack method):** Recommended — provides the lowest value possible.
  - **1 (Official service method):** Use only if you encounter issues with mode 2.

- **Vmin:** 550–620 mV
  - Typically not worth adjusting, as you should always use max RAM.

- **Vmin RAM OC:** AUTO

- **Vmax:** 800 mV

- **Voltage Offset:** 5–15
  - Test with 5, 10, or 15 when using UV2.
  - Some GPUs may require **0** for stability.


## RAM Settings

- **DRAM Timing:**
  - **0 — AUTO_ADJ:** Auto-adjust MTC table with LPDDR4 3733 Mbps specs, 16Gb density. Change timing with Advanced Config (Default).
  - **1 — AUTO_ADJ_HP:** Same as AUTO_ADJ, but with RAM power-down disabled.

  > **ℹ️ Tip:** AUTO_ADJ_HP improves latency, but some RAM modules may not handle it well.
  > - First, find your max RAM clocks and timings with **AUTO_ADJ**.
  > - Then test AUTO_ADJ_HP. If stable, use it — otherwise, stick to AUTO_ADJ.

- **DVB Shift:** 1–5
  - Boosts SoC voltage to help stabilize RAM, especially at high frequencies (2400 MHz+).


### RAM Configuration Based on Tier List

| Tier | RAM ID       | Ram Clock | VDD2   | VDDQ  | Common Timings           | Super Tight (ST) Timings  |
|------|--------------|-----------|--------|-------|--------------------------|---------------------------|
| GOD  | NEI/NEE/x267 | 2500–2933 | 1175 mV| 640 mV| (3-3-2) 2-5-5-4-6        | (4-4-4) 3-7-6-5-6          |
| GOD  | WT:B         | 2466–2600 | 1175 mV| 600 mV| (4-4-5) 5-2-6-5-6        | (6-6-7) 7-2-6-5-6          |
| S    | AA-MGCL/MGCR | 2300–2600 | 1175 mV| 640 mV| (4-4-5) 5-5-6-7-6        | (4-4-8) 6-5-7-8-6          |
| A    | WT:F         | 2400–2533 | 1175 mV| 600 mV| (4-4-2) 5-4-6-3-6        | (5-5-4) 5-5-6-5-6          |
| B    | AM-MGCJ      | 2300–2466 | 1175 mV| 640 mV| (3-2-4) 2-4-4-4-6        | (4-3-8) 2-5-4-4-6          |
| B    | WT:E         | 2300–2466 | 1175 mV| 600 mV| (2-2-2) 2-4-4-4-6        | (3-5-3) 3-5-4-5-6          |
| C    | AB-MGCL      | 2133–2500 | 1175 mV| 640 mV| (4-4-4) 4-4-5-6-6        | (4-4-8) 5-5-6-8-6          |
| D    | NME          | 2133–2333 | 1175 mV| 640 mV| (2-2-1) 0-1-4-3-6        | (3-3-4) 0-1-4-4-6          |


### RAM Tuning Notes

> **💡 Extra Headroom:** For an additional 66–100 MHz, try **1212.5 mV**. This can also help with tighter timings.

> **🧪 Testing Method:**
> 1. Start by setting **DVB = 4** using the common preset.
> 2. Test **ST (Super Tight) timings**.
> 3. If ST fails, relax timings one by one in this order: `t8 → t1 → t2 → t3 → t6 → t7 → t4 → t5`.
> 4. For pushing beyond ST, apply the same incremental approach.

> **⚡ Performance:** ST timings provide enhanced performance over common timings.

> **⚠️ Stability Notes:**
> - Lower **T5** or **T6** if you encounter issues.
> - RAM contributes the most to overall performance — prioritize finding your maximum frequency first.
> - Rarely, some modules may fail even with common timings. If so, lower timings until stable.

# Clock Settings(Safe)

### Mariko Max Safe on Battery [HAC-001(-01), HEG-001]
*Switch units available from August 2019 and beyond, includes OLED & requires modchip*
- **CPU:** 1963MHz
- **GPU:** 998MHz
- **RAM:** 2133MHz-2500MHz+ (whatever is stable, 2400MHz is recommended if stable for best battery life to performance ratio.)
 !!! warning ** Note:** Drawing over 8.6W on battery will cause battery issues. Please avoid doing that for extended periods!

### Switch Lite Max Safe Clocks on Battery [HDH-001]
- **CPU:** 1785MHz
- **GPU:** 921MHz
- **RAM:** 2133MHz-2500MHz+ (whatever is stable, 2400MHz is recommended if stable for best battery life to performance ratio.)
 !!! warning  ** Note:** Drawing over 6.5W on battery will cause battery issues. Please avoid doing that for extended periods!

!!! note Switch Lite limits are lower due to the 12W board power limit, but counts as Mariko for all other purposes.

### Mariko Max Clocks Docked and Plugged [HAC-001(-01), HEG-001]
*Switch units available from

 August 2019 and beyond, includes OLED & requires modchip*
- **CPU:** 
  - 2397MHz on CPU speedo < 1600
  - 2499MHz on CPU speedo ≥ 1600
  - 2601MHz on CPU speedo ≥ 1700
- **GPU:**
  - Sched **off**: 1228MHz (safe with 1228MHz voltage < 800 mV, otherwise use 1152MHz)
  -  Sched **on**: 1267MHz (safe with 1228MHz voltage < 800 mV)
  - 1228MHz sched **off** outperforms 1267MHz sched **on**, so it's recommended.
 - **RAM:**
   - 2133MHz-3000MHz+ (whatever is stable)

### Switch Lite Max Clocks Plugged [HDH-001]
- **CPU:**
  - 1963MHz on CPU Speedo < 1650
  - 2397MHz on CPU speedo ≥ 1650
- **GPU:**
  - Sched **off**: 1228MHz (safe with 1228MHz voltage < 800 mV, otherwise use 1152MHz)
  -  Sched **on**: 1267MHz (safe with 1228MHz voltage < 800 mV)
  - 1228MHz sched **off** outperforms 1267MHz sched **on**, so it's recommended.
- **RAM:**
  - 2133MHz-2800MHz+ (whatever is stable)

!!! note Switch Lite limits are lower due to the 12W board power limit, but counts as Mariko for all other purposes.

---

# Troubleshooting

**My Switch won't boot into EMUNAND after I have installed SWITCHCRAFT:**

- Your atmosphere version is likely not up-to-date, update your atmosphere version.
- CPU UV level is too high, lower it or set it to 0.

**My configs are not being applied:**
- Ensure you reboot your console after changing settings in SWITCHCRAFT.

**I can't set my clocks above 1785/921/1600:**
- Your kip is not being loaded, check if it is located in `/atmosphere/kips`
- Your hekate_ipl.ini file is not set up correctly:
   - Validate that your boot entry contains `kip1=atmosphere/kips/loader.kip`
   - It has to be below `pkg3=atmosphere/package3` (or fss0)

# Need Help with Setup?

###Follow this [guide](https://rentry.co/howtoget60fps) for a step-by-step setup.
