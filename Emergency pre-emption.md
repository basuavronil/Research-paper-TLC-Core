<img width="1189" height="566" alt="image" src="https://github.com/user-attachments/assets/fdfb8292-89c0-4eff-9090-4eb1086795ca" />

# Emergency Preemption Methodology & FSM Response

## One-Line Summary

**High-priority emergency signals trigger an immediate interrupt that forces the main FSM to abort regular cycles, fast-track to safe clearance, and grant an instant green phase to the emergency corridor.**

## Key Concepts Breakdown

### 1. Preemption Signal (Override Metric)

* **What it represents:** A high-priority input signal triggered by approaching emergency vehicles (e.g., ambulances, fire trucks, police cars) via optical, radio, or acoustic sensors.

* **Priority Level:** Highest priority input in the system—overrides normal adaptive timing, pedestrian requests, and night modes.

## 2. Core FSM Response Mechanism

1. **Interrupt Detection:** The **Emergency Preemption Module** continuously monitors input lines. Upon receiving a valid trigger, it sends a high-priority override command to the **Main FSM**.

2. **Safe Phase Termination:**

   * **If current phase is ALREADY Green for emergency lane:** The FSM extends the green phase until the vehicle passes.

   * **If current phase is Red for emergency lane:** The FSM immediately terminates the active green phase on conflicting lanes, executing a shortened, safe clearance sequence (Yellow $\rightarrow$ All-Red).

3. **Preemption Execution & Recovery:**

   * The FSM forces the emergency lane to **Green** while keeping all conflicting lanes strictly **Red**.

   * Once the preemption signal clears, the FSM resets to a default baseline state (or initial sequence phase) to resume standard adaptive cycling safely.

## Quick Reference for Presentation / Study

* **Emergency Trigger (**$\text{Active}$**)** $\rightarrow$ Priority Override Triggered $\rightarrow$ **FSM Aborts Active Phase (Safe Yellow/Red)** $\rightarrow$ Immediate Green for Emergency Lane.

* **Emergency Trigger (**$\text{Cleared}$**)** $\rightarrow$ Preemption Latch Resets $\rightarrow$ **FSM Returns to Baseline Cycle**.

