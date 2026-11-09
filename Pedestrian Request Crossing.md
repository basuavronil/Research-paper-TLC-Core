
<img width="1117" height="532" alt="image" src="https://github.com/user-attachments/assets/db6f6d2e-5523-4b08-aa33-00b9b3706e3e" />


# Pedestrian Request Methodology & FSM Response

## One-Line Summary

**The Pedestrian Request module latches button pushes and signals the main FSM to safely extend the green phase and activate dedicated walk indicators during the matching direction cycle.**

## Key Concepts Breakdown

### 1. Green-Phase Extension Latch (Input Metric)

* **What it represents:** An asynchronous pedestrian crosswalk button press that is safely caught and held by a hardware flip-flop latch until the FSM processes it.

* **Objective:** Ensure pedestrian requests are never missed while keeping crosswalk activation safely synchronized with vehicle traffic signals.

## 2. Core FSM Response Mechanism

1. **Request Latching:** When a pedestrian presses the button, the **Green-Phase Extension Latch** captures the signal and holds it high until the FSM reaches the corresponding direction's turn.

2. **Phase Extension & Walk Activation:**

   * **If active vehicle phase matches request direction:** The FSM extends the current green light timer by a set duration to grant pedestrians sufficient crossing time.

   * **Output Assertion:** The FSM asserts the dedicated `ped_walk` output line, lighting up the pedestrian crossing indicator while holding conflicting vehicle lines at red.

3. **Latch Reset & Normal Sequencing:**

   * Once the extended pedestrian walk cycle completes, the FSM automatically clears (resets) the request latch and transitions back to standard yellow/red sequence timing.

## Quick Reference for Presentation / Study

* **Button Pressed** $\rightarrow$ Request Latched $\rightarrow$ **FSM Synchronizes Cycle** $\rightarrow$ `ped_walk` Output High & Green Phase Extended $\rightarrow$ Latch Resets.
