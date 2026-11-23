# OS Laboratory Activity 3
## Multilevel Queue and Real-Time CPU Scheduling

### Student Information
- **Name:** Ariane Martin
- **Course and Section:** [BCA151 - B186.1]
- **Subject:** BCA151 – Operating Systems
- **Instructor:** [Maria Fe Bahinting]
- **Date Submitted:** November 14, 2026

---

## I. Introduction

CPU scheduling is an important function of an operating system. It determines which process or task will use the CPU and when it will execute.

This laboratory activity implements three CPU scheduling algorithms using Python: Multilevel Queue (MLQ), Rate Monotonic Scheduling (RMS), and Earliest Deadline First (EDF).

The activity demonstrates how different scheduling algorithms manage processes, allocate CPU time, and handle task deadlines. It also uses Gantt charts and performance measurements to analyze the scheduling results.

## II. Objectives

The objectives of this laboratory activity are:

1. Understand the concepts of Multilevel Queue, Rate Monotonic Scheduling, and Earliest Deadline First.
2. Implement Multilevel Queue scheduling using Round Robin and First Come First Served.
3. Implement preemptive Rate Monotonic Scheduling.
4. Implement preemptive Earliest Deadline First scheduling.
5. Generate and interpret Gantt charts.
6. Calculate CPU utilization, waiting time, turnaround time, and deadline compliance.
7. Practice creating, managing, and documenting Python programs using GitHub.

## III. Scheduling Algorithms

### A. Multilevel Queue (MLQ)

Multilevel Queue Scheduling divides processes into different queues based on their type or priority.

For this implementation:
- Queue 1 contains interactive processes and uses Round Robin with a time quantum of 2 ms.
- Queue 2 contains batch processes and uses First Come First Served (FCFS).
- Queue 1 has higher priority than Queue 2.
- A Queue 1 process can interrupt a running Queue 2 process.

### B. Rate Monotonic Scheduling (RMS)

Rate Monotonic Scheduling is a fixed-priority real-time scheduling algorithm. Tasks with shorter periods receive higher priorities.

For this implementation:
- T1 has the highest priority because its period is 4 ms.
- T2 has the next priority because its period is 5 ms.
- T3 has the lowest priority because its period is 10 ms.
- The simulation uses preemptive scheduling with 1 ms intervals.

### C. Earliest Deadline First (EDF)

Earliest Deadline First is a dynamic-priority real-time scheduling algorithm. It selects the ready task with the earliest absolute deadline.

For this implementation:
- Tasks are selected based on their absolute deadlines.
- Absolute Deadline = Release Time + Relative Deadline.
- A newly released task may preempt the currently running task if it has an earlier deadline.
- The simulation uses preemptive scheduling with 1 ms intervals.

## IV. Program Implementation

The laboratory contains three Python programs:

| Program | Description |
|---|---|
| `multilevel_queue/mlq.py` | Implements Multilevel Queue using Round Robin and FCFS. |
| `real_time_scheduling/rms.py` | Implements preemptive Rate Monotonic Scheduling. |
| `real_time_scheduling/edf.py` | Implements preemptive Earliest Deadline First scheduling. |

Each program generates a Gantt chart and displays scheduling results in the terminal.

## V. Test Data

### A. MLQ Test Data

| Process | Arrival Time | Burst Time | Queue |
|---|---:|---:|---:|
| P1 | 0 | 5 | 1 |
| P2 | 1 | 4 | 1 |
| P3 | 0 | 6 | 2 |
| P4 | 2 | 3 | 2 |
| P5 | 3 | 2 | 1 |

Queue 1 uses Round Robin with a 2 ms time quantum, while Queue 2 uses FCFS.

### B. RMS and EDF Test Data

| Task | Execution Time (C) | Period (T) | Deadline (D) |
|---|---:|---:|---:|
| T1 | 1 ms | 4 ms | 4 ms |
| T2 | 1 ms | 5 ms | 5 ms |
| T3 | 2 ms | 10 ms | 10 ms |

Both real-time scheduling simulations run for 20 ms.

## VI. Results and Discussion

### A. Multilevel Queue Scheduling

The MLQ implementation successfully scheduled interactive and batch processes using different scheduling policies.

**Results:**
- Average Turnaround Time: 12.0 ms
- Average Waiting Time: 8.0 ms
- Queue 1 processes were given priority over Queue 2 processes.

The results demonstrate how different process queues can use different scheduling policies depending on their requirements.

### B. Rate Monotonic Scheduling

The RMS implementation successfully scheduled periodic tasks based on their fixed priorities.

**Results:**
- CPU Utilization: 65.0%
- RMS Sufficient Utilization Bound: 77.98%
- Sufficient-Bound Test: PASS
- Deadline Misses: 0

The result shows that the task set passed the RMS sufficient utilization-bound test. All task instances completed within their deadlines during the simulation.

### C. Earliest Deadline First Scheduling

The EDF implementation successfully scheduled tasks based on their earliest absolute deadlines.

**Results:**
- CPU Utilization: 65.0%
- Classical EDF Utilization Test: PASS
- Deadline Misses: 0

All task instances met their deadlines during the simulation. The utilization was below 100%, satisfying the classical EDF utilization test under the assumptions of this laboratory.

## VII. Algorithm Comparison

| Criteria | MLQ | RMS | EDF |
|---|---|---|---|
| Scheduling basis | Queue priority | Task period | Absolute deadline |
| Priority | Based on queue | Fixed | Dynamic |
| Scheduling type | Different policies per queue | Preemptive | Preemptive |
| Main purpose | Organizing different process types | Periodic real-time tasks | Deadline-based real-time tasks |
| Deadline monitoring | Not inherent | Yes | Yes |

MLQ is useful when processes are classified into different queues. RMS is suitable for periodic real-time tasks with fixed priorities. EDF is useful when tasks need to be prioritized according to their deadlines.

## VIII. Guide Questions and Answers

**37. What is the main difference between Multilevel Queue and Multilevel Feedback Queue Scheduling?**

Multilevel Queue Scheduling assigns processes to fixed queues, while Multilevel Feedback Queue allows processes to move between queues depending on their behavior and execution.

**38. Why are different scheduling algorithms used for different process queues?**

Different processes have different requirements. Interactive processes need faster responses, while batch processes can use other scheduling policies.

**39. How does RMS choose which task to execute?**

RMS chooses the ready task with the shortest period because it has the highest fixed priority.

**40. Why is RMS considered a fixed-priority scheduling algorithm?**

RMS is fixed-priority because each task receives its priority based on its period, and that priority does not change during execution.

**41. How does EDF choose the next task to execute?**

EDF selects the ready task with the earliest absolute deadline.

**42. Why is EDF considered a dynamic-priority scheduling algorithm?**

EDF is dynamic because task priorities can change as new tasks are released and deadlines change.

**43. What happens if a newly released task has an earlier deadline than the currently running task under EDF?**

The newly released task can preempt the currently running task because it has an earlier deadline.

**44. Why is CPU utilization important in real-time scheduling?**

CPU utilization measures how much processing time is needed by tasks. It helps determine whether the processor can handle the workload.

**45. Can a system with CPU utilization below 100% still miss a deadline? Explain.**

Yes. A system can still miss a deadline because of task dependencies, scheduling overhead, or an unfavorable task workload. Utilization alone does not guarantee that every scheduling configuration is feasible.

**46. Which algorithm would you recommend for periodic real-time tasks, RMS or EDF? Justify your answer.**

EDF is recommended when flexibility in task deadlines is important because it dynamically prioritizes tasks based on their deadlines. However, RMS is also useful because it is simpler and assigns fixed priorities based on task periods.

## IX. Conclusion

This laboratory activity demonstrated three CPU scheduling algorithms: Multilevel Queue, Rate Monotonic Scheduling, and Earliest Deadline First. The Python implementations successfully generated Gantt charts and scheduling results. The experiments helped demonstrate how different scheduling methods manage CPU resources, process priorities, and task deadlines.
