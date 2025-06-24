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

### GPU Scheduling:
- **On:** Caps gpu usage at ~96.7%
- **Off:** Caps gpu usage at  ~99.7%
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

## CPU Settings
- **Boost Clock:**
  - 2400 MHz (Low Speedo or High Freq UV 1-5)
  - 2600 MHz (Speedo > 1650 or High Freq UV 6+)
- **Undervolt Mode:** 1-8(start with 4) (Increase if stable, find your highest stable value. In case console doesn't boot, lower it.)
- **High Freq UV:** 5-10 (Find your highest stable value). Just a few units can do 11-12, test carefully.
- **Low Freq Vmin:** 590mv
- **High Freq Vmin:** 720-750mv (Test for lower values if your CPU bin is good)
- **Voltage Limit:** 1120mv (safe), 1160mv (use with caution)
- **Table Config:** AUTO 

## GPU Settings
- **Undervolt Mode:** 2
- **DVFS:** 2(hijack method) or 1(official service method). Use 1 only in case you have issues since 2 should provide the lowest value possible.
- **Vmin:** 550-620mv(you shouldn't bother with this, as you MUST use always max ram)
- **Vmin RAM OC:** AUTO
- **Vmax:** 800mv
- **Voltage Offset:** 5-15 (Test 5, 10, or 15 with UV2, but check stability first. Some gpu must use 0.)

## RAM Settings
- **DRAM Timing:**
  - 0: AUTO_ADJ: Auto adjust mtc table with LPDDR4 3733 Mbps specs, 16Gb density. Change timing with Advanced Config (Default)
  - 1: AUTO_ADJ_HP: Same as AUTO_ADJ with ram power down disabled.

  - **Recommended:** AUTO_ADJ_HP due better latency.

- **DVB Shift:** 1-5 (Boosting the SoC voltage helps stabilize RAM, especially at high frequencies like 2400MHz+).

### RAM Configuration Based on Tier list:

| Tier | RAM ID   | Ram Clock | VDD2  | VDDQ  | Common Timings          | Super Tight (ST) Timings     |
|------|----------|-----------|-------|-------|---------------------------|---------------------------|
| GOD  | NEI/NEE/x267  | 2500-2933 | 1175mv| 640mv | (3-3-2) 2-5-5-4-6      | (4-4-4) 3-7-6-5-6      |
| GOD  | WT:B     | 2466-2600 | 1175mv| 600mv | (4-4-5) 5-2-6-5-6      | (6-6-7) 7-2-6-5-6      |
| S    | AA-MGCL/MGCR  | 2300-2600 | 1175mv| 640mv | (4-4-5) 5-5-6-7-6      | (4-4-8) 6-5-7-8-6      |
| A    | WT:F     | 2400-2533 | 1175mv| 600mv | (4-4-2) 5-4-6-3-6      | (5-5-4) 5-5-6-5-6      |
| B    | AM-MGCJ  | 2300-2466 | 1175mv| 640mv | (3-2-4) 2-4-4-4-6     | (4-3-8) 2-5-4-4-6       |
| B    | WT:E     | 2300-2466 | 1175mv| 600mv | (2-2-2) 2-4-4-4-6     | (3-5-3) 3-5-4-5-6      |
| C    | AB-MGCL  | 2133-2500 | 1175mv| 640mv | (4-4-4) 4-4-5-6-6      | (4-4-8) 5-5-6-8-6      |
| D    | NME      | 2133-2333 | 1175mv| 640mv | (2-2-1) 0-1-4-3-6     | (3-3-4) 0-1-4-4-6      |

!!! note If you want to do 66-100mhz more, try 1212.5mv. Also it can help with timings.

To find your maximum frequency, start by setting DVB to 4 using the common preset. Next, test ST. If ST fails, incrementally increase the timings one by one in this order: t8, t1, t2, t3, t6, t7, t4 and t5. Be sure to test each timing adjustment individually. If you want to go beyond ST timings, apply the same methodology as described above.

Super Tight timings provide enhanced performance over the common timings.
!!! note **Note**: Lower T5 or T6 in case you have issues.
!!! note RAM delivers the most performance, so prioritize finding your maximum frequency first.

# Clock Settings(Safe)

### Mariko Max Safe on Battery [HAC-001(-01), HEG-001]
*Switch units available from August 2019 and beyond, includes OLED & requires modchip*
- **CPU:** 1963MHz
- **GPU:** 998MHz
- **RAM:** 2133MHz-2500MHz+ (whatever is stable)
 !!! warning ** Note:** Drawing over 8W on battery will cause battery issues. Please avoid doing that for extended periods!

### Switch Lite Max Safe Clocks on Battery [HDH-001]
- **CPU:** 1785MHz
- **GPU:** 921MHz
- **RAM:** 2133MHz-2500MHz+ (whatever is stable)
 !!! warning  ** Note:** Drawing over 6.5W on battery will cause battery issues. Please avoid doing that for extended periods!

!!! note Switch Lite limits are lower due to the 12W board power limit, but counts as Mariko for all other purposes.

### Mariko Max Clocks Docked and Plugged [HAC-001(-01), HEG-001]
*Switch units available from

 August 2019 and beyond, includes OLED & requires modchip*
- **CPU:** 2397MHz on CPU speedo < 1650, 2601MHz on CPU speedo ≥ 1650 with undervolt
- **GPU:** 1228MHz (1267MHz and above on GPU speedo ≥ 1650 with undervolt, otherwise lower)
- **RAM:** 2133MHz-3000MHz+ (whatever is stable)

### Switch Lite Max Clocks Plugged [HDH-001]
- **CPU:** 1963MHz (2397MHz on CPU speedo ≥ 1650 with undervolt)
- **GPU:** 1228MHz(1267MHz on GPU speedo ≥ 1650 with undervolt, otherwise lower)
- **RAM:** 2133MHz-2800MHz+ (whatever is stable)

!!! note Switch Lite limits are lower due to the 12W board power limit, but counts as Mariko for all other purposes.

---

# Troubleshooting

**My Switch won't boot into EMUNAND after I have installed SWITCHCRAFT:**

- Your atmosphere version is likely not up-to-date, update your atmosphere version.
- CPU UV level is too high, lower it or set it to 0.

# Need Help with Setup?

###Follow this [guide](https://rentry.co/howtoget60fps) for a step-by-step setup.
