# THIS IS A BACKUP AND MAY BE OUTDATED
# [FOLLOW THIS GUIDE INSTEAD](https://rentry.co/howtoteststability/): [https://rentry.co/howtoteststability/](https://rentry.co/howtoteststability/)

# Stability Testing Guide

**WIP Guide by Dominatorul**
Some parts of this guide were contributed by ChanseyIsTheBest and Lightos_

---

## Table of Contents

1. [CPU Testing](#cpu-testing)
   - [Recommended Games for CPU Undervolting](#recommended-games-for-testing-cpu-undervolting-uv)

2. [GPU Testing](#gpu-testing)
   - [Signs of GPU Voltage Instability](#signs-of-gpu-voltage-instability)
   - [Examples of GPU Voltage Instability](#examples-of-gpu-voltage-instability)

3. [RAM Testing](#ram-testing)
   - [Recommended Games for RAM Stability Testing](#recommended-games-for-testing-ram-stability)
   - [Example of RAM Instability](#example-of-ram-instability)

4. [Ultracam Benchmark Test](#ultracam-benchmark-test)

---

## CPU Testing

The only reliable artificial CPU stress test application is **`StressNX`**. To test your CPU:

1. Press `X` to set the test mode to `matrixpod`.
2. Press `Y` to enable **`burning`** mode.
3. Press `A` to start the test.
4. Test all frequencies for about 15-30 seconds and check if it remains stable.

### Recommended Games for Testing CPU Undervolting (UV)

1. **`Need for Speed: Hot Pursuit`**
   - **Scenario:** If the CPU undervolt is unstable, the game will crash in the main menu on the map at 1963 MHz and 60 fps (credits to B3711).
   - **Testing Procedure:** Leave the game running on the desired frequency for 15-30 seconds while on the map screen. Test every frequency carefully to ensure stability.

2. **`Kirby and the Forgotten Land`**
   - **Scenario:** This game is suitable for testing low CPU Vmin using stock clock speed (1020 MHz).
   - **Testing Procedure:** Run the game docked at 60 fps to observe for crashes or instability. Let it run for hours; it may crash after prolonged testing.

---

## GPU Testing

Testing GPU stability using GPU voltage offsets or undervolting (UV3) can be challenging, as no reliable artificial stress tests are available on the Horizon Operating System (HOS). Therefore, we rely on games known to be sensitive to unstable GPU voltages.

### Signs of GPU Voltage Instability

- **Visual Glitches:** "Disco lights," white flashes, or color distortions indicate that the GPU voltage is too low.
- **Crashes and Hangs:** If the GPU voltage is insufficient, games might crash or hang without showing visual glitches.

### Examples of GPU Voltage Instability

1. **`Convergence: A League of Legends Story`**
   - **Very Low GPU Voltage:** Observe color distortion and blue light.
   - **Slightly Higher but Still Low GPU Voltage:** Persistent blue light.

2. **`SIFU`**
   - **Too Low GPU Voltage:** Subtle white flashes, especially on the left side of the screen.

3. **`Pikmin 3 Deluxe`**
   - **Low GPU Voltage and Vmin:** Pixel corruption in the bottom left corner of the image.

4. **`Monster Hunter Rise`**
    - **Too low GPU Voltage:** Freezes after playing for an extended period of time. (Credits to Arcdelta)

5. **`Xenoblade Chronicles X`**
    - **Too low GPU Voltage:** Game crashes on main page. (Credits to Happy)

---

## RAM Testing

Test at maximum (safe) clocks docked to ensure maximum possible load.
If you can't dock your switch, use `ReverseNX`.

### Recommended Games for Testing RAM Stability

1. **`Monster Hunter Stories 2: Wings of Ruin`**
   - **Scenario:** Start the game and let the first two cutscenes run. Look for artifacts.

2. **`The Legend of Zelda: Tears of the Kingdom (TOTK)`**
   - **Scenario:** Run the game for about an hour; crashes, freezes, or hangs indicate unstable RAM.
   Version 1.0.0 is particularly sensitive.

   [TOTK Ultracam Test and Benchmark](https://rentry.co/ultracam)

3. **`Red Dead Redemption`**
   - **Scenario:** Run the game for about an hour to detect instability.

4. **`Borderlands 3`**
   - **Scenario:** Monitor for pixel corruption, crashes, or hangs after extended play.

5. **`Borderlands: The Pre-Sequel`**
   - **Scenario:** Similar to `Borderlands 3`, it stresses RAM heavily.

6. **`Nier Automata`**
   - **Scenario:** Especially effective with 60 FPS cheats or graphical mods.

7. **`Kirby and the Forgotten Land`**
   - **Scenario:** Monitor for crashes or graphical corruption after extended play.

### Example of RAM Instability

- **Game:** `Borderlands 3`
   - **Unstable RAM:** Pixel corruption or crashes during play.

---

## Benchmarking Ram

`MemtoolkitNX` is mainly recommended for RAM benchmarking (such as fine-tuning memory timings), but it can also be used for CPU and GPU tests.
To run it, launch the tool via title override with its default settings.
!!! danger `MemtoolkitNX` is not reliable for stability testing — use it only for benchmarking purposes.

## Ultracam Benchmark Test

The **Ultracam** benchmark test is one of the best tools to assess system performance and stability under heavy load. It is highly recommended for testing RAM, GPU, and overall system stability. For details, visit this guide: [TOTK Ultracam Test and Benchmark](https://rentry.co/ultracam).
