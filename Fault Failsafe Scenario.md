
<img width="1098" height="497" alt="image" src="https://github.com/user-attachments/assets/3f88cbbb-2543-4ca2-a0a9-f398caf6ef7b" />

# Fault Detector & Failsafe Methodology & FSM Response

## One-Line Summary

**The Fault Detector continuously evaluates FSM state transitions for invalid steps, immediately asserting a hard override to force all signal outputs into a safe, all-red blinking state during hardware anomalies.**

## Key Concepts Breakdown

### 1. Illegal Step & Hardware Monitoring (Input Metric)

* **What it represents:** Hardware monitoring logic that inspects the current 8-bit FSM state and signal outputs to detect illegal state jumps, conflicting green signals, or timer counter overruns.

* **Objective:** Ensure catastrophic signal failures (e.g., simultaneous North-South Green and East-West Green) are physically impossible on the hardware level.

## 2. Core FSM & Hardware Response Mechanism

1. **Continuous Inspection:** The **Fault Detector** module reads state bits (`NS[1:0]`, `EW[1:0]`, and main FSM sequencer bits) concurrently with every clock cycle.

2. **Anomaly Detection & Trigger:**

   * **If an Illegal State occurs:** The detector flags an invalid condition (e.g., dual green vectors, missing sequence steps, hardware logic corruption).

3. **Failsafe Override Execution:**

   * **Signal Intercept:** The module immediately drives the dedicated `fault_out` line high and overrides standard FSM outputs.

   * **All-Red Blink Mode:** The hardware shifts to a hardcoded failsafe mode, toggling the `blink` output signal to flash all signal directions red, warning drivers that the intersection logic has failed.

## Quick Reference for Presentation / Study

* **State Anomaly (**$\text{Detected}$**)** $\rightarrow$ Fault Detector Triggers $\rightarrow$ **FSM Main Logic Overridden** $\rightarrow$ `fault_out` High & `blink` Active (All-Red Failsafe).
