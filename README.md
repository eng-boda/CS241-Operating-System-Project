<div align="center">

# 🚀 CPU Scheduling Simulator
## 📂 CS241 - Operating System Project

</div>

## 📌 Project Overview
This simulator focuses on the critical balance between **Fairness** and **Efficiency**. It provides a side-by-side comparison using interactive Gantt charts, ready queue states, and detailed performance metrics.

### Key Algorithms Supported:
* **Round Robin (RR):** Ensures equal opportunity by allocating fixed time slices (quantums) to every process.
* **SRTF (Shortest Remaining Time First):** Optimizes performance by always executing the process with the least remaining time.

---

## 📊 Fairness vs. Efficiency: The Comparison

| Feature | Round Robin (RR) | SRTF |
| :--- | :--- | :--- |
| **Goal** | Fair sharing of CPU. | Minimize average waiting time. |
| **Starvation** | **No starvation;** all processes get CPU time regularly. | **Risk of starvation** for long processes. |
| **Efficiency** | Performance depends on quantum size (q). | Mathematically best for minimizing waiting/turnaround time. |
| **Response Time** | Guaranteed response within one time quantum. | Short jobs respond fast; long jobs may wait significantly. |

---

## 🧪 Testing Scenarios & Analysis
The simulator includes 5 built-in scenarios to demonstrate the core mechanics of each algorithm:

### 🔹 Scenario A: Mixed Workload (The Standard Case)
Testing how algorithms handle a typical workload with varied arrival and burst times.
* **Data:** P1(0,8), P2(1,4), P3(2,9), P4(3,5) | **Quantum:** 3
* **Goal:** Observe the basic trade-off where SRTF minimizes waiting time while RR ensures fairness.
* **Key Outcome:** SRTF generally achieves a lower average waiting time, but RR provides more consistent response times.

### 🔹 Scenario B: Quantum Sensitivity
Demonstrating how the **Time Quantum** size is the primary performance driver for Round Robin.
* **Data:** Four processes with identical burst times (6 units) arriving at the same time.
* **Test Case:**
    * **Small Q=2:** Highly responsive, but increased context-switching overhead.
    * **Large Q=6:** Lower overhead, but starts behaving like FCFS (First-Come-First-Served).

### 🔹 Scenario C: Short-Job Heavy
Visualizing how **SRTF** takes immediate advantage of short burst times by preempting long-running tasks.
* **Data:** One long job (10 units) vs. several very short ones (1-2 units).
* **Result:** SRTF significantly reduces average waiting time by "clearing" short tasks out of the system instantly.

### 🔹 Scenario D: Interactive-Style Fairness
Testing first response time by having all processes arrive simultaneously at $t=0$.
* **Goal:** Prove why RR is preferred for interactive systems; it guarantees every process gets its first CPU turn within a predictable window.

### 🔹 Scenario E: Robust Validation (The Error Case)
Testing the simulator's logic and data integrity layer.
* **Input:** Invalid arrival times (negative values) or zero/invalid quantum sizes.
* **Result:** The system catches errors through a validation layer, preventing crashes and displaying user-friendly error messages.

---

## 📊 Quick Comparison Summary

| Metric | Round Robin (RR) | SRTF | Winner |
| :--- | :--- | :--- | :--- |
| **Avg Waiting Time** | Higher | Lower (Optimized) | 🏆 **SRTF** |
| **Avg Response Time** | Lower (Fast) | Higher for long jobs | 🏆 **RR** |
| **Fairness** | High (Equal Slices) | Low (Short-job bias) | 🏆 **RR** |
| **Starvation Risk** | None | Possible for long jobs | 🏆 **RR** |

---

## 🛡️ Robust Validation Layer
The simulator is built with data integrity in mind. It includes a validation layer that detects:
* Invalid (negative) arrival times.
* Invalid (zero) quantum sizes.
* Ensures the program never crashes due to unexpected input.

---

## 🧠 Final Verdict
* **Choose Round Robin** if you are building an **Interactive System** where fairness and quick response times for all users are vital.
* **Choose SRTF** for **Batch Processing** or high-throughput environments where minimizing the total wait time is the ultimate goal.
