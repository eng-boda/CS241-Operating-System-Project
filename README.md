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
The simulator includes pre-built scenarios to stress-test each algorithm:

### 🔹 Scenario A: Mixed Workload
Tests how algorithms handle a typical mix of arrival and burst times.
- **Result:** SRTF generally wins on average waiting time, while RR maintains a smaller waiting time spread (Fairness).

### 🔹 Scenario B: Quantum Sensitivity
Demonstrates how changing the Time Quantum (q) alters RR behavior.
- **Small q:** Highly responsive but high context-switching overhead.
- **Large q:** Low overhead but behaves like First-Come-First-Served (FCFS).

### 🔹 Scenario C: Short-Job Heavy
Shows SRTF’s power in preempting long jobs to clear short tasks instantly.

### 🔹 Scenario D: Interactive Fairness
Proves RR's superiority in interactive systems by guaranteeing a quick first turn for every process.

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
