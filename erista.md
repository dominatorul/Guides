# Erista OC Guide

*Made with love by Dominatorul. Some parts of this guide belong to ChanseyIsTheBest and Lightos_*

---

## Table of Contents
- [Safety Disclaimer](#safety-disclaimer)
- [Erista Limits](#erista-limits)
- [Monitoring Your Switch](#monitoring-your-switch)
- [Checking Speedo and RAM Type](#checking-speedo-and-ram-type)
- [RAM Types](#ram-types)
- [OC Settings for Switchcraft](#oc-settings-for-switchcraft)
   - [CPU Settings](#cpu-settings)
   - [GPU Settings](#gpu-settings)
   - [RAM Settings](#ram-settings)
- [Clock Settings](#clock-settings)
   - [Erista Max Plugged](#erista-max-plugged-hac-001-01-heg-001)
   - [Erista Max Safe Clocks on Battery](#erista-max-safe-clocks-on-battery-hdh-001)
- [Troubleshooting & Advice](#troubleshooting)
- [How to test stability](https://rentry.co/howtoteststability)
---

# Safety Disclaimer
!!! info **All overclocking is unsafe as you are pushing the system outside of its original design, however the level of risk is dependent on how much you overclock and stay within the limits of the chip and the hardware.**

!!! danger **Unstable RAM overclocking can cause SYSNAND/EMUNAND corruption and SD card corruption, particularly if done on SYSNAND. Test the overclock settings on EMUNAND and back it up before installing Switchcraft.**

---

# Erista Limits

### Charger IC Limit:
- Erista has a 15A PMIC, usually this limit won't be reached during overclocking.
- The main limiting factor for Erista units is the 18W limit.

### Erista CPU Limits:
- The board limit of 18W is reached at 1785MHz without any UV or 2091MHz with CPU UV1.

### Erista GPU Limits:
- The board limit of 18W is reached at 921MHz without GPU UV with moderate speedos.

### GPU Scheduling:
- **On:** Caps gpu usage at ~96.7%
- **Off:** Caps gpu usage at  ~99.7%
!!! danger  ** Warning:** Disabling GPU Scheduling will slightly increase power draw. Use it with caution.

---

#Monitoring Your Switch
- Use status monitor overlay to indicate if you've bypassed the charger IC limit (e.g., -1W displayed while charging).
- To get the best results, be sure your battery is 10-90% to display the real charging
- If the battery is above 90%, power drawn from the charger gets reduced.
- A slight negative power draw (roughly -0.1W) is fine if the battery is above 90%
- A higher negative power draw (~-0.5W) is not safe
- For accurate results, test with a lower battery.

---

#Checking Speedo and RAM Type

1. Boot Hekate.
2. Go to Console Info > HW & Fuses.
3. Note your DRAM ID, CPU Speedo 0, CPU Speedo 2, and SoC Speedo.

CPU/GPU Speedos range from approximately 1980 to 2200, with SoC speedos ranging from approximately 1899 to 2050. An Erista with a higher speedo requires less voltage to meet the same clock speed compared to another Switch with a lower speedo. A CPU/GPU speedo of 2100 is generally considered good.

---

#RAM Types

There are various RAM types for Erista, and better types can reach higher clocks, require lower voltages, and support tighter timings at the same clocks compared to worse types. Not only do RAM types matter, but RAM bin matters, meaning that worse RAM types can outperform higher RAM types. Here are some RAM types:

- Samsung MGCH
- Hynix NLE
- Micron WT:C

Almost all Erista units have Samsung MGCH RAM. Hynix NLE and Micron WT:C are rare but can potentially achieve slightly higher clocks, test carefully.

---

# OC Settings for Switchcraft

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
## RAM Settings
- **DRAM Timing:**
  - 0: AUTO_ADJ: Auto adjust mtc table with LPDDR4 3733 Mbps specs, 16Gb density. Change timing with Advanced Config (Default)
  - 1: AUTO_ADJ_HP: Same as AUTO_ADJ with ram power down disabled.

  - **Recommended:** AUTO_ADJ_HP due better latency.

- **DVB Shift:** 1-4 (Boosting the SoC voltage helps stabilize RAM, especially at high frequencies like 2400MHz+).
#### Samsung MGCH
- **RAM Clock:** 1862-2133Mhz (Very good bins may reach slightly higher clocks, clocks up to 2246Mhz are potentially possible with overvolting)
- **VDD2:** 1175–1237 mV (The module is rated for 1175 mV. You can overvolt slightly if you want, since 1237 mV is allowed in L4T, so it's assumed to be safe, 1175mV is guaranteed to be safe.)
- **Timings:** Common (4-4-4) 0-1-5-4-6 or ST(Super tight) (4-5-9) 1-2-6-4-6. Super Tight timings provide enhanced performance over the common timings.

To find your maximum frequency, start by setting DVB to 2 using the common preset. Next, test ST. If ST fails, incrementally increase the timings one by one in this order: t8, t1, t2, t3, t6, t7, t4 and t5. Be sure to test each timing adjustment individually. If you want to go beyond ST timings, apply the same methodology as described above.
Super Tight timings provide enhanced performance over the common timings.
!!! note **Note**: Lower T5 or T6 or T3 in case you have issues.
!!! note RAM delivers the most performance, so prioritize finding your maximum frequency first.


# Clock Settings

### Erista Max Plugged [HAC-001(-01), HEG-001]
*Switch units available from August 2019 and beyond, includes OLED & requires modchip*
- **CPU:** 2295MHz (Use only with UV5 on good speedo), 2091MHz (Use only with UV3-5), 1785MHz (UV is recommended)
- **GPU:** 998MHz (Use it only with UV2, try to avoid going over 1000mv), 921MHz (safe, use it with undervolt)
- **RAM:** 1862MHz-2133MHz+ (whatever is stable and within 1175mv VDD2) (HEAVILY DEPENDENT ON RAM TYPE)

### Erista Max Safe Clocks on Battery [HDH-001]
- **CPU:** 1785MHz
- **GPU:** 460MHz
- **RAM:** 1862MHz-2133MHz+ (whatever is stable and within 1175mv VDD2) (HEAVILY DEPENDENT ON RAM TYPE)
!!! warning **Note:** Drawing over 8.6W on battery will cause battery issues. Please avoid doing that for extended periods!

---

For stability testing, follow this [guide](https://rentry.co/howtoteststability/)

#Troubleshooting

**My Switch won't boot into EMUNAND after I have installed SWITCHCRAFT:**
- Your atmosphere or EOS version is likely not up-to-date, update your atmosphere or eos version.
- CPU UV level is too high, lower it or set it to 0.

**My configs are not being applied:**
- Ensure you reboot your console after changing settings in SWITCHCRAFT.

# Need Help with Setup?

###Follow this [guide](https://rentry.co/howtoget60fps) for a step-by-step setup.
