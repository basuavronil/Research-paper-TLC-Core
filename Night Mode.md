
<img width="1098" height="497" alt="image" src="https://github.com/user-attachments/assets/abe4b9ee-2376-4ab0-b6bd-8224aa67b844" />

# Night Mode Methodology & FSM Response

## One-Line Summary

**Night Mode activates a parameterized cycle shifter that scales down standard green/red phase durations to minimize unnecessary wait times during low-volume off-peak hours.**

## Key Concepts Breakdown

### 1. Off-Peak Parameterization (Input Metric)

* **What it represents:** A scheduled or ambient-light triggered operational state indicating minimal traffic density across all directions.
* **Objective:** Reduce cycle latency and eliminate prolonged stops at empty intersections.

## 2. Core FSM Response Mechanism

1. **Mode Activation:** The **Night Mode** module receives an external time/mode trigger and signals the **Main FSM** to switch to an optimized timing parameters register.
2. **Cycle Shifting & Duration Reduction:**
   * **Timer Threshold Adjustment:** Base green-light phase thresholds are reduced to a low fixed minimum (e.g., short 5–10 second cycles).
   * **Rapid Sequencing:** The FSM cycles rapidly between directions, granting immediate access whenever a vehicle is detected without waiting for long fixed timers to expire.
3. **Optional Flashing Operation:**
   * If configured for flashing mode during ultra-low traffic hours, the FSM bypasses full signal sequencing entirely and shifts to continuous yellow/red warning blinks (or hands control over to the fault/blink module).

## Quick Reference for Presentation / Study

* **Night Mode (**$\text{Active}$**)** $\rightarrow$ Parameterized Cycle Shifter Enabled $\rightarrow$ **FSM Shortens Phase Timers** $\rightarrow$ Rapid Rotations & Reduced Idle Time.
