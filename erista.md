# Erista OC Guide

*Made with love by Dominatorul. Some parts of this guide belong to ChanseyIsTheBest.*

---

## Table of Contents
1. [Safety Disclaimer](#safety-disclaimer)
2. [Erista Limits](#erista-limits)
3. [Monitoring Your Switch](#monitoring-your-switch)
4. [Checking Speedo and RAM Type](#checking-speedo-and-ram-type)
5. [RAM Types](#ram-types)
6. [OC Settings for Switchcraft](#oc-settings-for-switchcraft)
   - [CPU Settings](#cpu-settings)
   - [GPU Settings](#gpu-settings)
   - [RAM Settings](#ram-settings)
7. [Clock Settings](#clock-settings)
   - [Erista Max Plugged](#erista-max-plugged-hac-001-01-heg-001)
   - [Erista Max Safe Clocks on Battery](#erista-max-safe-clocks-on-battery-hdh-001)
8. [Troubleshooting & Advice](#troubleshooting)

---

## Safety Disclaimer
!!! info **All overclocking is unsafe as you are pushing the system outside of its original design, however the level of risk is dependent on how much you overclock and stay within the limits of the chip and the hardware.**

!!! danger **Unstable RAM overclocking can cause SYSNAND/EMUNAND corruption and SD card corruption, particularly if done on SYSNAND. Test the overclock settings on EMUNAND and back it up before installing Switchcraft.**

---

# Erista Limits

### Erista CPU Limits:
- The Erista CPU limit of 15A is reached at 1785MHz without any UV or 2091MHz with CPU UV1.

### Erista GPU Limits:
- The Erista GPU limit of 15A is reached at 921MHz without GPU UV with moderate speedos.
!!! danger **Be extremely careful if you disable GPU scheduling. This will hit the PMIC limit very hard!**

### Charger IC Limit:
- 18W limit restricts overclocking for Erista units. This is the main limiting factor, but the PMIC current limits for CPU and GPU will be reached first.

---

## Monitoring Your Switch
- Use status monitor overlay to indicate if you've bypassed the charger IC limit (e.g., -1W displayed while charging).
- To get the best results, be sure your battery is 10-90% to display the real charging

---

## Checking Speedo and RAM Type

1. Boot Hekate.
2. Go to Console Info > HW & Fuses.
3. Note your DRAM ID, CPU Speedo 0, CPU Speedo 2, and SoC Speedo.

Speedos range from approximately 1980 to 2200, with SoC speedos ranging from approximately 1899 to 2050. An Erista with a higher speedo requires less voltage to meet the same clock speed compared to another Switch with a lower speedo. A speedo of 2100 is generally considered good.

---

## RAM Types

There are various RAM types for Erista, and better types can reach higher clocks, require lower voltages, and support tighter timings at the same clocks compared to worse types. Not only do RAM types matter, but RAM bin matters, meaning that worse RAM types can outperform higher RAM types. Here are some RAM types:

- Samsung MGCH
- Hynix NLE
- Micron WT:C

---

## OC Settings for Switchcraft

### CPU Settings
- **Boost Clock:** 2091MHz if you use UV3, otherwise use 1785MHz
- **Undervolt Mode:** 1-5 (use the max that is stable)
- **Vmin:** 800
- **Voltage Limit:** 1225mv

### GPU Settings
- **Undervolt Mode:** 2
- **Vmin:** 740-780mv
- **Voltage Offset:** 0-30
!!!note If you want to safely use 998Mhz gpu, you need to keep gpu volt under 950 (slightly differs depending on iddq and temperature)
### RAM Settings
- **DRAM Timing:**
  - 0: AUTO_ADJ: Auto adjust mtc table with LPDDR4 3733 Mbps specs, 16Gb density. Change timing with Advanced Config (Default)
  - 1: ~~AUTO_ADJ_LV: Less tight timings. It can help achieve higher frequencies or lower voltages.~~
  - 2: ~~AUTO_ADJ_LV_HP: LV mode with slightly tighter timings~~
  - 3: NO_ADJ: Use 1600 mtc table without adjusting (Timing becomes tighter if you raise dram clock).

  - **Recommended:** AUTO_ADJ

- **DVB Shift:** 1-4 (Boosting the SoC voltage helps stabilize RAM, especially at high frequencies like 1996MHz+).

#### Samsung MGHC
- **RAM Clock:** 1862-2133Mhz
- **VDD2:** 1175mv
- **Timings:** Common (3-3-2) 0-4-4-0-6 or ST (4-4-4) 1-4-5-0-6 
- **HP mode:** 1
---

## Clock Settings

### Erista Max Plugged [HAC-001(-01), HEG-001]
*Switch units available from August 2019 and beyond, includes OLED & requires modchip*
- **CPU:** 2295MHz (Use only with UV5 on good speedo), 2091MHz (Use only with UV3-5), 1785MHz (UV is recommended)
- **GPU:** 998MHz (Use it only with UV2, try to avoid going over 1000mv), 921MHz (safe, use it with undervolt)
- **RAM:** 1862MHz-2133MHz+ (whatever is stable and within 1175mv VDD2) (HEAVILY DEPENDENT ON RAM TYPE)

### Erista Max Safe Clocks on Battery [HDH-001]
- **CPU:** 1785MHz
- **GPU:** 460MHz
- **RAM:** 1862MHz-2133MHz+ (whatever is stable and within 1175mv VDD2) (HEAVILY DEPENDENT ON RAM TYPE)
!!! warning **Note:** Drawing over 8W on battery will cause battery issues. Please avoid doing that for extended periods!

---

## Troubleshooting

**My Switch won't boot into EMUNAND after I have installed SWITCHCRAFT:**
- Your atmosphere version is likely not up-to-date, update your atmosphere version.
- CPU UV level is too high, lower it or set it to 0.
