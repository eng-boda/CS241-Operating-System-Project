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

## 📊 Required Comparison Focus

### 1️. Fairness versus Efficiency

| Feature | Round Robin (RR) | Shortest Remaining Time First (SRTF) |
| :--- | :--- | :--- |
| **Fairness** | 1. Every process gets a fixed time slice (quantum q). <br> 2. **No starvation** → all processes get CPU time regularly. <br> 3. Ensures equal opportunity for all processes. | 1. Short processes are always favored. <br> 2. Long processes may suffer from **starvation** (they keep getting preempted if shorter jobs keep arriving). <br> 3. A process might wait indefinitely if shorter jobs keep coming. |
| **Efficiency** | 1. Performance depends heavily on time quantum ($q$). <br>    - Large $q$ → behaves like **FCFS** (Weak Interactivity and  Low Overhead). <br>       - Small $q$ → behaves like **RR** (Fast Responsive and High Overhead). <br> 2.Higher context switching overhead than SRTF. <br> 3. Does not minimize waiting time. | 1. Minimizes average waiting time and turnaround time. <br> 2. Always runs the process with the least remaining time (Best performance). <br> 3. Overhead due to frequent preemption. |

### 2️. Effect of Time Slicing versus Shortest-Job Preference

| Feature | Round Robin (RR) | Shortest Remaining Time First (SRTF) |
| :--- | :--- | :--- |
| **CPU Allocation** | Divides CPU time into fixed time slices (quantum q). | Always selects the process with the smallest remaining time. |
| **Treatment of Jobs** | Ignores how short or long a job is → even very short jobs may wait for their turn. | Short jobs finish very quickly. |
| **Goal** | Fair sharing of CPU. | Minimize average waiting time. |
| **Overall Effect** | CPU time is shared evenly, but not optimized for job length. | CPU time is optimized for shortest jobs, not shared evenly. |

### 3. Effect on first response time

| Feature | Round Robin (RR) | SRTF |
| :--- | :--- | :--- |
| **Effect on first response time** | Each process is guaranteed to receive CPU time within one time quantum, ensuring that no process waits too long before its first execution. | Prioritizes shorter processes, which means that short jobs can get an immediate response, but longer processes may experience significant delays before their first execution. |

### 4. Effect of quantum size on Round Robin behavior

| Feature | Small quantum(q) | Large quantum(q) |
| :--- | :--- | :--- |
| **Effect** | Fair and highly responsive but causes high overhead due to frequent context switching. | Efficient with low overhead but less responsive and behaves like FCFS. |

### 5. Whether SRTF gives a strong advantage to short jobs

| Feature | SRTF |
| :--- | :--- |
| **Waiting Time** | Very low for short processes |
| **Execution Behavior** | Short jobs are executed immediately |
| **Fairness** | Low (biased toward short jobs) |

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

## 🧠 Required Analysis Questions

### 1. Which algorithm gave better average waiting time?
SRTF (Shortest Remaining Time First) typically produces a lower average waiting time. By prioritizing processes with the shortest remaining burst, it clears tasks from the system faster, thereby reducing the total time other processes spend waiting in the queue.

### 2. Which algorithm gave better response time?
Round Robin (RR) generally provides better (lower) average response time. Its time-slicing mechanism ensures that every process receives a portion of the CPU shortly after arrival, which is critical for interactive systems.

### 3. Did Round Robin appear fairer across all processes?
Yes, Round Robin is considered fairer because it allocates CPU time equally through a fixed time quantum. This prevents 'starvation,' where long processes are indefinitely delayed by shorter ones, a risk inherent in SRTF.

### 4. Did SRTF complete short jobs faster?
Yes, SRTF is designed specifically to optimize the completion of short jobs. By preempting longer processes whenever a shorter job arrives, it ensures that minimal burst time tasks exit the system as quickly as possible.

### 5. How did the selected quantum affect the Round Robin results?
The time quantum is the primary performance driver for RR. A small quantum improves responsiveness but increases overhead due to context switching. A large quantum reduces overhead but can make the system feel sluggish, eventually behaving like FCFS.

### 6. Which algorithm would you recommend for the tested workload, and why?
If the workload consists of time-sensitive interactive tasks, Round Robin is recommended for its fairness and response time. If the goal is high throughput and efficiency for a batch of mixed tasks, SRTF is the superior choice for minimizing average wait times.

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
