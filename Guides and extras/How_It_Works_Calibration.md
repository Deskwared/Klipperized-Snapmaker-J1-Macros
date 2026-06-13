# Automated IDEX Calibration Workflow

Your Snapmaker J1s IDEX configuration has been fundamentally rewritten to seamlessly utilize electrical continuity datum pads built into the machine. Instead of manual paper-dragging tests, the printer dynamically polls for high-precision physical closures to perfectly align your Z-Offsets, Bed Tramming, and XY Toolhead offsets. 

This guide breaks down exactly how to operate the new unified testing GUI found in your touchscreen under **"Calibrations"**.

---

## Step 1: Global Preparation (MANDATORY)

Before engaging in **any** calibration logic, the physical environment must be completely scrubbed. Cooled plastic isolated on the tip of the nozzle will instantly block the electrical circuits from triggering when tapping the datum pads!

**Workflow:**
1. Navigate to **Calibrations**.
2. Tap **1. Calibrations Prep**.
3. The printer will pre-heat the bed and both nozzles.
4. It will physically spread both toolheads cleanly to the left and right center layout. 
5. **ACTION REQUIRED**: Take a brass wire brush and aggressively scrub BOTH nozzles completely clean of any plastic ooze. 

*Once the nozzles are fully clean, immediately proceed to one of the following testing modules in the Sub-Menu while the machine is hot.*

---

## Step 2: Bed Tramming (Leveling)

This process automatically guides you through adjusting the 3 built-in bed screws using real-time polling to ensure maximum horizontal stability. 

**Workflow:**
1. Open the **Bed Tramming** menu. 
2. Tap **2. Auto-Probe Bed**.
3. The printer will drop the nozzle to the fixed rear corner and record it as your exact "Baseline".
4. It will then sweep to the physical **Left Pad** and enter an aggressive physical jumping loop. 
5. Look at your KlipperScreen interface. You will see a readout identical to: `Pad Z: -3.05  Ref: -3.00`
6. **ACTION REQUIRED**: Reach under the bed and mechanically twist the Left bed screw. 
   - Watch the numbers dynamically update on the screen as the printer repeatedly punches the pad. 
   - You want your `Pad Z` to perfectly match your `Ref`. 
7. Once the algorithm detects that the values match `2` times in a row, it automatically confirms stability and sweeps to the **Right Pad**. 
8. Repeat the mechanical twisting process for the right knob. 
9. Upon stable lock, the printer natively terminates the loop and parks itself!

---

## Step 3: Z-Offset Calibration

This module digitally aligns the vertical length of the secondary toolhead (T1 - Right) to precisely match the absolute distance of the primary toolhead (T0 - Left). 

**Workflow:**
1. Open the **Z-Offset** menu.
2. Tap **2. Auto-Probe Z**.
3. T0 (Left) will extend, tap the datum pad, save its coordinate mathematically as the perfect baseline, and dynamically drop away.
4. T1 (Right) will aggressively sweep into position over the exact same pad and begin the physical polling loop.
5. As it bounces, watch your KlipperScreen. You will see something like: `Pad Z: -2.90  Ref: -3.00`.
6. **ACTION REQUIRED**: Using the physical mechanical height dial wheel physically embedded into the Right toolhead, twist the dial to raise or lower the nozzle height.
   - You are granted `4.0mm` of massive clearance during its bounce loop so you have plenty of room to dial the wheel without the machine crowding your fingers. 
7. Keep tuning the wheel until the graphic numbers match identically.
8. Once the algorithm hits `2` identical continuous reads, it aggressively drives T1 safely upward to `Z=100` and suspends itself completely. 
9. **ACTION REQUIRED**: Tap **3. Z Calibration Complete** in the UI. 
   - The printer finalizes the mathematical saves into Klipper's persistent variables, physically retracts T1, parks both heads out of bounds, and kills all thermal heaters. 

---

## Step 4: XY Offset Calibration

This algorithm guarantees that when Klipper requests T1 to drop to an XY coordinate natively defined by T0, it is flawlessly vertically stacked without horizontal ghosting.

**Workflow:**
1. Open the **XY Offsets** menu. 
2. Tap **2. Auto-Probe XY**.
3. **Stand back.** The printer operates 100% autonomously here. 
   - It leverages a specialized 3-stage adaptive horizontal bumping loop:
   - **Coarse Pass (`0.2mm`)**: Rapid horizontal probing to accurately establish the approximate bounds of the cavity slot.
   - **Fine Pass (`0.05mm`)**: A tighter approach algorithm calculating sub-measurements.
   - **Ultra-Fine Pass (`0.01mm`)**: Sub-micron locking of the exact physical cavity wall.
4. It repeats this pattern for all four walls symmetrically against T0, then physically tags in T1 and repeats the pattern blindly. 
5. When complete, Klipper injects the calculated differences natively into `[save_variables]` and overrides standard IDEX `SET_GCODE_OFFSET` variables to ensure slicer toolchanges never wipe them out. 
6. Homing is refreshed and the printer turns itself off. 
