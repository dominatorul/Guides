# How to Test Stability

**WIP Guide by Dominatorul.**  
Some parts from this guide belong to ChanseyIsTheBest.

## CPU Testing

The only reliable artificial CPU stress test application is **`StressNX`**. To test your CPU:

1. Press `X` to set the test mode to `matrixpod`.
2. Press `Y` to enable **`burning`** mode.
3. Press `A` to start the test.
4. Test all frequencies for about 15-30 seconds and check if the voltage result is stable.


Recommended Games for Testing CPU Undervolting (UV)

1. `Need for Speed: Hot Pursuit`   
   - **Scenario:** If the CPU undervolt is unstable, the game will crash in the main menu on the map at 1963 MHz and 60 fps (credits to B3711).  
   - **Testing Procedure:** Leave the game running on the desired frequency for 15-30 seconds while on the map screen. Test every frequency carefully to ensure stability.

2. `Kirby and the Forgotten Land`  
   - **Scenario:** This game is suitable for testing low CPU Vmin  using stock clock speed (1020mhz). 
   - **Testing Procedure:** Run the game docked at 60 fps to observe for crashes or instability. Let it run for hours, it will crash after a few hours.

## GPU Testing

Testing GPU stability using GPU voltage offsets or undervolting (UV3) can be challenging, as there are no good artificial stress tests available on the Homebrew Operating System (HOS). Therefore, we rely on games known to be more sensitive to unstable GPU voltages.

### Signs of GPU Voltage Instability

- **GPU Voltage Glitches:** Look for "disco lights," white flashes, or color distortions. These artifacts indicate that the GPU voltage is too low.  
- **Crash and Hangs:** If the GPU voltage is too low, games might crash or hang without showing any visual glitches.

#### Examples of GPU Voltage Instability

1. `Convergence: A League of Legends Story`  
   - **Very Low GPU Voltage:** Notice the color distortion and the blue light.  
   ![Convergence: A League of Legends Story, very low GPU volt](https://i.imgur.com/jVr5RgC.png)  
   - **Slightly Higher but Still Low GPU Voltage:** Observe the persistent blue light.  
   ![Convergence: A League of Legends Story, higher but still too low GPU volt](https://i.imgur.com/bMkC3xy.png)  

2. `SIFU` 
   - **Too Low GPU Voltage:** Look for subtle white flashes, especially on the left side of the screen.  
   ![SIFU, too low GPU volt, subtle white flashes](https://i.imgur.com/UdZ5wmH.png)  

3. `Pikmin 3 Deluxe`  
   - **Low GPU Voltage and Vmin:** Check for pixel corruption in the bottom left corner of the image.  
   ![Pikmin 3 Deluxe, too low GPU volt and vmin](https://i.imgur.com/BfW4Cb4.png)  

*Convergence and SIFU images credit Medel, Pikmin 3 Deluxe image credit AnimatedSwine37.*

## RAM Testing
A good application to test the ram is **`MemToolkitNX`**.

0. Set the cpu and the ram to max to gather the highest bandwidth possible.
1. Set the test type using `DPAD right`  to **`2x Memtester + BW Burn-in`**.
2. Press `A` to start the test.
3. Run the test 200-500 loops.
 !!!note This is good to find some errors, test the stability in game!

### Recommended Games for Testing RAM Stability

!!!note Do those tests in docked mode for higher resource usage.

1. **Game:** `Monster Hunter Stories 2: Wings of Ruin`  
   - **Scenario:** To test for unstable RAM, start the game and let the first 2 cutscenes to run. Look for artifacts.
   - **Signs of Instability:** Freezing, crashes, or unexpected restarts.

2. **Game:** `The Legend of Zelda: Tears of the Kingdom (TOTK)`  
   - **Scenario:** To test for unstable RAM, leave your Switch running for approximately one hour on this game, it will crash, hang, or freeze when using unstable RAM. These games typically use a large amount of system resources.
   - **Signs of Instability:** Crashes, freezes, or hangs.

TODO: Ultracam test explaination.
3. **Game:** `Red Dead Redemption`  
   - **Scenario:** To test for unstable RAM, leave your Switch running for approximately one hour on this game, it will crash, hang, or freeze when using unstable RAM. These games typically use a large amount of system resources.  
   - **Signs of Instability:** Crashes, hangs, or graphical corruption.

4. **Game:** `Borderlands 3`  
   - **Scenario:** To test for unstable RAM, leave your Switch running for approximately one hour on this game, it will crash, hang, or freeze when using unstable RAM. These games typically use a large amount of system resources.  
   - **Signs of Instability:** Pixel corruption, crashes, or system hangs.  

5. **Game:** `Borderlands: The Pre-Sequel`  
   - **Scenario:** Similar to `Borderlands 3`, it uses substantial resources, which can trigger instability in RAM.  
   - **Signs of Instability:** Crashes, graphical corruption, or system hangs.

6. **Game:** `Nier Automata`  
   - **Scenario:** Especially effective with 60 FPS cheats or graphical modifications that increase load.  
   - **Signs of Instability:** Crashes, hangs, or visual glitches during high-stress scenes.

7. . **Game:** `Kirby and the Forgotten Land`  
   - **Scenario:** To test for unstable RAM, leave your Switch running for approximately one hour on this game, it will crash, hang, or freeze when using unstable RAM. These games typically use a large amount of system resources.  
   - **Signs of Instability:** Crashes, hangs, or graphical corruption.
Unstable RAM can cause graphical glitches, but more often leads to crashes or hangs.

#### Example of RAM Instability

- `Borderlands 3` 
  - **Unstable RAM:** Notice the pixel corruption on the right side of the image.  
  ![Borderlands 3, unstable RAM](https://i.imgur.com/QT9aHr7.png)  

*Borderlands 3 image credit Medel.*

---

This guide should help you effectively test the stability of your system's CPU, GPU, and RAM to ensure optimal performance and prevent potential issues.
