<img width="1216" height="527" alt="image" src="https://github.com/user-attachments/assets/baba6673-bf0d-446c-b278-f70ec6722d77" />

# Adaptive Green Light Methodology & FSM Response     

## One-Line Summary
**Higher pulse density (traffic sensor frequency) signals heavy traffic, prompting the core FSM to dynamically extend green-phase timer counts before triggering a state transition.**

--- 
  
## Key Concepts Breakdown

### 1. Pulse Density (Input Metric)
* **What it represents:** The frequency of vehicle detection pulses received from sensors (e.g., induction loops, optical sensors, or radar) over a set time window.
* **High Density:** High pulse rate $\rightarrow$ Heavy traffic volume detected.  
* **Low Density:** Low pulse rate $\rightarrow$ Light traffic volume or empty road.

---

## 2. Core FSM Response Mechanism

1. **Pulse Sampling:** The adaptive timer module continuously counts input pulses from the sensors during the active green cycle.
2. **Dynamic Scaling:** 
   * **If Density > Threshold:** The module increases the target counter value of the green phase timer, holding the current green signal longer.
   * **If Density $\le$ Threshold:** The module retains or reduces the default timer limit to prevent empty lane idling.
3. **State Transition Execution:**
   * Once the dynamically calculated timer count is reached, the **Main FSM (8-bit Sequencer)** sequences to the yellow/red phase and transfers priority to the next traffic signal. 

---

## Quick Reference for Presentation / Study

* **Sensor Pulses ($\uparrow$)** $\rightarrow$ High Traffic Density $\rightarrow$ **Adaptive Timer Extends Green Phase** $\rightarrow$ FSM Delays Transition.
* **Sensor Pulses ($\downarrow$)** $\rightarrow$ Low Traffic Density $\rightarrow$ **Adaptive Timer Keeps Minimum Green** $\rightarrow$ FSM Transitions Faster.
