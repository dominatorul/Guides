# Mariko OC Guide

*Made with love by Dominatorul. Some parts of this guide belong to ChanseyIsTheBest.*

---

## Table of Contents
1. [Safety Disclaimer](#safety-disclaimer)
2. [Mariko Limits](#mariko-limits)
3. [Monitoring Your Switch](#monitoring-your-switch)
4. [Checking Speedo and RAM Type](#checking-speedo-and-ram-type)
5. [RAM Tiers](#ram-tiers-higher-is-better)
6. [OC Settings for Switchcraft](#oc-settings-for-switchcraft)
   - [CPU Settings](#cpu-settings)
   - [GPU Settings](#gpu-settings)
   - [RAM Settings](#ram-settings)
7. [Clock Settings](#clock-settings)
   - [Mariko Max Safe on Battery](#mariko-max-safe-on-battery-hac-001-01-heg-001)
   - [Switch Lite Max Safe Clocks on Battery](#switch-lite-max-safe-clocks-on-battery-hdh-001)
   - [Mariko Max Clocks Docked and Plugged](#mariko-max-clocks-docked-and-plugged-hac-001-01-heg-001)
   - [Switch Lite Max Clocks Plugged](#switch-lite-max-clocks-plugged-hdh-001)
8. [Troubleshooting](#troubleshooting)

---

## Safety Disclaimer
!!! info ** Overclocking is inherently risky as it pushes the system beyond its original design. The risk level depends on how much you overclock and whether you stay within the limits of the chip and hardware.**

!!! danger **Unstable RAM overclocking can cause SYSNAND/EMUNAND corruption and SD card corruption, particularly if done on SYSNAND. Test the overclock settings on EMUNAND and back it up before installing Switchcraft.**

---

# Mariko Limits

### Mariko CPU Limits:
- 5A limit reached at 2397MHz (CPU UV1) or 2295MHz (< 1650 CPU speedo).
- Use higher UV levels to avoid exceeding the PMIC limit.

### Mariko GPU Limits:
- 10A limit reached at 1228MHz (GPU UV1) with moderate speedos (1650 GPU clock).
- Disabling GPU scheduling overloads the PMIC, potentially causing damage.

### GPU Scheduling:
- **On:** ~96.7%
- **Off:** ~99.7%
!!! danger  ** Warning:** Disabling GPU Scheduling will significantly increase power draw. Use it with caution.

### Charger IC Limit:
- 18W limit restricts overclocking for both Erista and Mariko units (12W on Switch Lite). This is the main limiting factor, but the PMIC current limits for CPU and GPU will be reached first.

---

## Monitoring Your Switch
- Use status monitor overlay to indicate if you've bypassed the charger IC limit (e.g., -1W displayed while charging).
- To get the best results, be sure your battery is 10-90% to display the real charging

---

## Checking Speedo and RAM Type

1. Boot Hekate.
2. Go to Console Info > HW & Fuses.
3. Note your DRAM ID, CPU Speedo 0, CPU Speedo 2, and SoC Speedo.
   - Speedos typically range from 1450 to 1750. A higher speedo means less voltage is needed for the same clock speed. A speedo of 1650 is generally considered good.

---

## RAM Tiers (Higher is better)
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

## CPU Settings:
- **Boost Clock:**
  - 2400 MHz (Low Speedo or High Freq UV 1-5)
  - 2600 MHz (Speedo > 1650 or High Freq UV 6+)
- **Undervolt Mode:** 1-4 (Increase if stable, find your highest stable value)
- **High Freq UV:** 6-10 (Find your highest stable value). Just a few units can do 11-12, test carefully.
- **Low Freq Vmin:** 590mv
- **High Freq Vmin:** 720-750mv (Test for lower values if your CPU bin is good)
- **Voltage Limit:** 1120mv (safe), 1160mv (use with caution)

## GPU Settings:
- **Undervolt Mode:** 2
- **Vmin:** AUTO (0)
- **Vmax:** 800mv
- **Speedo:** (Input your value from HW & Fuses)
- **Voltage Offset:** 0 (Test 5, 10, or 15 with UV2, but check stability first)

## RAM Settings:
- **DRAM Timing:**
  - 0: AUTO_ADJ: Auto adjust mtc table with LPDDR4 3733 Mbps specs, 16Gb density. Change timing with Advanced Config (Default)
  - 1: ~~AUTO_ADJ_LV: Less tight timings. It can help achieve higher frequencies or lower voltages.~~
  - 2: ~~AUTO_ADJ_LV_HP: LV mode with slightly tighter timings~~
  - 3: NO_ADJ: Use 1600 mtc table without adjusting (Timing becomes tighter if you raise dram clock).

  - **Recommended:** AUTO_ADJ

- **DVB Shift:** 1-4 (Boosting the SoC voltage helps stabilize RAM, especially at high frequencies like 2400MHz+).
- **HP mode:** 1

### RAM Configuration Based on Tier

| Tier | RAM ID   | Ram Clock | VDD2  | VDDQ  | Timings (Common)          | Timings (ST)              |
|------|----------|-----------|-------|-------|---------------------------|---------------------------|
| GOD  | NEI/NEE  | 2500-2900 | 1175mv| 640mv | (3-3-2) 2-5-5-4-6      | (4-4-4) 3-7-6-5-6      |
| GOD  | WT:B     | 2466-2600 | 1175mv| 600mv | (4-4-5) 5-2-6-5-6      | (6-6-7) 7-2-6-5-6      |
| S    | AA-MGCL/MGCR  | 2300-2566 | 1175mv| 640mv | (4-4-5) 5-5-6-7-6      | (4-4-8) 6-5-7-8-6      |
| A    | WT:F     | 2400-2566 | 1175mv| 600mv | (4-4-2) 5-4-6-3-6      | (5-5-4) 6-5-6-3-6      |
| B    | AM-MGCJ  | 2300-2466 | 1175mv| 640mv | (2-2-4) 3-4-4-4-6     | (4-3-7) 3-5-4-4-6       |
| B    | WT:E     | 2300-2466 | 1175mv| 600mv | (2-2-2) 5-4-5-2-6     | (3-3-2) 5-4-6-2-6      |
| C    | AB-MGCL  | 2133-2433 | 1175mv| 640mv | (4-4-4) 4-4-5-6-6      | (4-4-5) 5-5-6-6-6      |
| D    | NME      | 2133-2333 | 1175mv| 640mv | (2-2-1) 0-1-4-3-6     | (3-3-4) 0-1-4-4-6      |

---
!!! note **Note**: Lower T5 or T6 in case you have issues.
# Clock Settings

### Mariko Max Safe on Battery [HAC-001(-01), HEG-001]
*Switch units available from August 2019 and beyond, includes OLED & requires modchip*
- **CPU:** 1963MHz
- **GPU:** 998MHz
- **RAM:** 2133MHz-2500MHz+ (whatever is stable and within 1175mv VDD2)
 !!! warning ** Note:** Drawing over 8W on battery will cause battery issues. Please avoid doing that for extended periods!

### Switch Lite Max Safe Clocks on Battery [HDH-001]
- **CPU:** 1785MHz
- **GPU:** 921MHz
- **RAM:** 2133MHz-2500MHz+ (whatever is stable and within 1175mv VDD2)
 !!! warning  ** Note:** Drawing over 6.5W on battery will cause battery issues. Please avoid doing that for extended periods!

!!! note Switch Lite limits are lower due to the 12W board power limit, but counts as Mariko for all other purposes.

### Mariko Max Clocks Docked and Plugged [HAC-001(-01), HEG-001]
*Switch units available from

 August 2019 and beyond, includes OLED & requires modchip*
- **CPU:** 2295MHz on CPU speedo < 1650, 2601MHz on CPU speedo ≥ 1650 with undervolt
- **GPU:** 1152MHz (1228MHz and above on GPU speedo ≥ 1650 with undervolt, otherwise lower)
- **RAM:** 2133MHz-2500MHz+ (whatever is stable and within 1175mv VDD2)

### Switch Lite Max Clocks Plugged [HDH-001]
- **CPU:** 1963MHz (2295MHz on CPU speedo < 1650, 2397 on CPU speedo ≥ 1650 with undervolt)
- **GPU:** 998MHz (1228MHz on GPU speedo ≥ 1650 with undervolt, otherwise lower)
- **RAM:** 2133MHz-2500MHz+ (whatever is stable and within 1175mv VDD2)

!!! note Switch Lite limits are lower due to the 12W board power limit, but counts as Mariko for all other purposes.

---

# Troubleshooting

**My Switch won't boot into EMUNAND after I have installed SWITCHCRAFT:**

- Your atmosphere version is likely not up-to-date, update your atmosphere version.
- CPU UV level is too high, lower it or set it to 0.
