# Operating System – Module 2: Process Management and CPU Scheduling

These notes cover all the topics you listed in simple language, with examples, diagrams, scheduling algorithms, solved problems, and practice questions.

## 2.1 Introduction

An Operating System (OS) manages computer hardware and software resources. It acts as an interface between the user, applications, and hardware.

Examples: Windows, Linux, macOS, Android.

In process management, the OS manages running programs and decides which process gets CPU time.

Example: When you open Chrome, play music, and use Excel simultaneously, the OS manages these running applications and allocates CPU resources to them.

## 2.2 Process Concept and Process States

### What is a process?

A process is a program that is currently executing.

| Program                      | Process                               |
| ---------------------------- | ------------------------------------- |
| A set of stored instructions | A program in execution                |
| Passive entity               | Active entity                         |
| Stored as a file             | Uses CPU, memory, and other resources |
| Example: `calculator.exe`    | Calculator running on your computer   |

A process typically contains:

- Program code
- Data and variables
- CPU registers
- Program counter
- Stack and heap
- Process Control Block (PCB)

### What is a PCB?

A Process Control Block (PCB) is a data structure maintained by the OS to store information about a process.

It typically contains the process ID (PID), process state, CPU registers, scheduling information, memory information, and I/O status.

### Process states

New

Process is being created

Ready

Waiting for CPU allocation

Running

Currently using the CPU

Terminated

Execution finished

Waiting / Blocked

Waiting for I/O or an event

Simplified process-state diagram. Running processes may return to Ready or move to Waiting; a Waiting process returns to Ready when its event completes.

The five common states are:

| State             | Meaning                                     |
| ----------------- | ------------------------------------------- |
| New               | Process is being created                    |
| Ready             | Process is waiting for CPU time             |
| Running           | Process is executing on the CPU             |
| Waiting / Blocked | Process is waiting for I/O or another event |
| Terminated        | Process has finished execution              |

Example: You open a music player. It enters the Ready state, gets CPU time, and enters Running. When it waits for data from storage, it may enter Waiting. After the data arrives, it returns to Ready.

## 2.3 CPU-bound and I/O-bound Processes

| Feature          | CPU-bound                             | I/O-bound                                      |
| ---------------- | ------------------------------------- | ---------------------------------------------- |
| Main requirement | CPU processing                        | Input/output operations                        |
| CPU usage        | Long CPU bursts                       | Short CPU bursts                               |
| Typical tasks    | Video rendering, complex calculations | Reading files, keyboard input, database access |
| Common waiting   | Less I/O waiting                      | More I/O waiting                               |

CPU-bound example: A Python program performing millions of mathematical calculations.

I/O-bound example: A program downloading a file from the internet.

A process can have both CPU and I/O activity; the classification depends on which activity dominates its execution.

## 2.4 Operating System Services

An operating system provides services that help programs execute safely and efficiently.

Common services include:

1. User interface
2. Program execution
3. Process management
4. Memory management
5. File-system management
6. I/O device management
7. Security and protection
8. Error detection
9. Resource allocation
10. Accounting and monitoring

### 2.4.1 Process Management

Process management involves creating, scheduling, executing, and terminating processes.

Its responsibilities include:

- Creating and deleting processes.
- Suspending and resuming processes.
- Allocating CPU time.
- Supporting process synchronization.
- Supporting communication between processes.
- Handling deadlocks.

### 2.4.2 Thread Management

A thread is the smallest unit of CPU execution managed by the operating system's scheduler.

A process can contain multiple threads.

For example, a browser may use different threads for its user interface, page rendering, and background tasks.

| Process                                         | Thread                                                           |
| ----------------------------------------------- | ---------------------------------------------------------------- |
| Has its own process resources and address space | Shares the process's address space and resources                 |
| Generally heavier to create                     | Generally lighter to create                                      |
| Can contain multiple threads                    | Executes a sequence of instructions                              |
| Processes are isolated from one another         | Threads within one process can communicate through shared memory |

Threads improve responsiveness and can enable parallel execution on multicore processors.

## 2.5 CPU Scheduler

A CPU scheduler selects a process from the Ready queue for CPU execution.

The three traditional scheduling levels are:

### 2.5.1 Short-term scheduler

- Also called the CPU scheduler.
- Selects a ready process for execution.
- Runs frequently.
- Must make decisions quickly.

### 2.5.2 Medium-term scheduler

- Temporarily suspends processes.
- May swap processes out of memory and later bring them back.
- Helps manage memory pressure and the degree of multiprogramming.

### 2.5.3 Long-term scheduler

- Also called the job scheduler.
- Selects jobs to be admitted into the system for processing.
- Controls the degree of multiprogramming.
- Commonly discussed in batch operating systems.

### Dispatcher

The dispatcher hands CPU control to the process selected by the short-term scheduler.

Its functions include:

- Performing a context switch when required.
- Switching to the appropriate execution mode.
- Jumping to the correct instruction of the selected process.

The time required to stop one process and start another is associated with context-switch overhead.

| Component             | Main responsibility                                  |
| --------------------- | ---------------------------------------------------- |
| Long-term scheduler   | Decides which jobs enter the system                  |
| Medium-term scheduler | Suspends and resumes processes, often using swapping |
| Short-term scheduler  | Selects the next ready process for the CPU           |
| Dispatcher            | Transfers CPU control to the selected process        |

## 2.6 CPU Scheduling

CPU scheduling determines the order in which ready processes receive CPU time.

### 2.6.1 Preemptive scheduling

In preemptive scheduling, the OS can interrupt a running process and allocate the CPU to another process.

Examples:

- Round Robin (RR)
- Shortest Remaining Time First (SRTF)
- Preemptive Priority Scheduling

Advantages:

- Better responsiveness for interactive applications.
- Suitable for time-sharing systems.

Disadvantages:

- More context-switch overhead.
- Requires careful handling of shared resources.

### 2.6.2 Non-preemptive scheduling

In non-preemptive scheduling, a process keeps the CPU until it finishes its CPU burst or blocks for an event.

Examples:

- First Come, First Served (FCFS)
- Non-preemptive Shortest Job First (SJF)
- Non-preemptive Priority Scheduling

Advantages:

- Simple to implement.
- Lower scheduling-related interruption overhead.

Disadvantages:

- Long processes can make short processes wait.
- Interactive responsiveness may be poor.

## 2.7 Scheduling Algorithms

Before studying the algorithms, learn these terms.

| Term                  | Meaning                                     |
| --------------------- | ------------------------------------------- |
| AT — Arrival Time     | Time when a process enters the Ready queue  |
| BT — Burst Time       | Total CPU time required for the process     |
| CT — Completion Time  | Time when the process finishes              |
| TAT — Turnaround Time | Total time from arrival to completion       |
| WT — Waiting Time     | Total time spent waiting in the Ready queue |
| RT — Response Time    | Time from arrival until first CPU execution |

Formulas:

\\[ TAT = CT - AT \\]

\\[ WT = TAT - BT \\]

\\[ RT = \text{First CPU Start Time} - AT \\]

These formulas assume that burst time represents the total CPU execution time, without separately adding I/O or context-switch time.

Let's use the following dataset for the first three algorithms.

| Process | Arrival Time | Burst Time | Priority |
| ------- | ------------ | ---------- | -------- |
| P1      | 0            | 5          | 2        |
| P2      | 0            | 3          | 1        |
| P3      | 0            | 1          | 3        |

For FCFS, SJF, and SRTF, smaller arrival times and burst times determine scheduling according to the algorithm. Priority 1 is the highest priority in this example.

### 2.7.1 FCFS — First Come, First Served

FCFS executes processes in arrival order. It is a non-preemptive algorithm.

When arrival times are equal, assume the listed order is used.

For our dataset, the order is P1, P2, P3.

### FCFS Gantt chart

P1

0–5

P2

5–8

P3

8–9

0

5

8

9

| Process | AT | BT | CT | TAT = CT − AT | WT = TAT − BT |
| ------- | -- | -- | -- | ------------- | ------------- |
| P1      | 0  | 5  | 5  | 5             | 0             |
| P2      | 0  | 3  | 8  | 8             | 5             |
| P3      | 0  | 1  | 9  | 9             | 8             |
| Average |    |    |    | 7.33          | 4.33          |

Average waiting time:

\\[ \frac{0+5+8}{3}=4.33 \\]

Limitation: A long process at the beginning can make all shorter processes wait. This is known as the convoy effect.

### 2.7.2 SJF — Shortest Job First

SJF selects the ready process with the smallest CPU burst time. In its standard form, it is non-preemptive.

For our dataset, all processes arrive at time 0, so the execution order is P3, P2, P1.

### SJF Gantt chart

P3

0–1

P2

1–4

P1

4–9

0

1

4

9

| Process | AT | BT | CT | TAT  | WT   |
| ------- | -- | -- | -- | ---- | ---- |
| P1      | 0  | 5  | 9  | 9    | 4    |
| P2      | 0  | 3  | 4  | 4    | 1    |
| P3      | 0  | 1  | 1  | 1    | 0    |
| Average |    |    |    | 4.67 | 1.67 |

Average waiting time:

\\[ \frac{4+1+0}{3}=1.67 \\]

SJF minimizes average waiting time under the usual assumptions when all relevant jobs are available and their CPU burst lengths are known.

Limitation: The exact CPU burst length is often unknown, and long jobs may suffer starvation if short jobs keep arriving.

### 2.7.3 SRTF — Shortest Remaining Time First

SRTF is the preemptive version of SJF.

The scheduler selects the ready process with the smallest remaining CPU time. If a new process arrives with a shorter remaining time, it can preempt the running process.

Let's use a different dataset to demonstrate preemption.

| Process | Arrival Time | Burst Time |
| ------- | ------------ | ---------- |
| P1      | 0            | 7          |
| P2      | 2            | 4          |
| P3      | 4            | 1          |

Execution:

- Time 0–2: P1 executes; 5 units remain.
- Time 2: P2 arrives with 4 units, so it preempts P1.
- Time 2–4: P2 executes; 2 units remain.
- Time 4: P3 arrives with 1 unit and preempts P2.
- Time 4–5: P3 finishes.
- Time 5–7: P2 finishes.
- Time 7–12: P1 finishes.

### SRTF Gantt chart

P10–2

P22–4

P34–5

P25–7

P17–12

| Process | AT | BT | CT | TAT  | WT   |
| ------- | -- | -- | -- | ---- | ---- |
| P1      | 0  | 7  | 12 | 12   | 5    |
| P2      | 2  | 4  | 7  | 5    | 1    |
| P3      | 4  | 1  | 5  | 1    | 0    |
| Average |    |    |    | 6.00 | 2.00 |

For P1:

\\[ WT = 12-7-0=5 \\]

For P2:

\\[ WT = 7-4-2=1 \\]

For P3:

\\[ WT = 5-1-4=0 \\]

Limitation: Long processes can experience starvation when shorter processes repeatedly arrive.

### 2.7.4 RR — Round Robin Scheduling

Round Robin is a preemptive scheduling algorithm commonly associated with time-sharing systems.

Each process receives a fixed CPU time called a time quantum. If it does not finish within that quantum, it returns to the end of the Ready queue.

Example dataset:

| Process | AT | BT |
| ------- | -- | -- |
| P1      | 0  | 5  |
| P2      | 0  | 3  |
| P3      | 0  | 1  |

Assume a time quantum of 2 units and queue order P1, P2, P3.

Execution:

- P1: 0–2, 3 units remain.
- P2: 2–4, 1 unit remains.
- P3: 4–5, finishes.
- P1: 5–7, 1 unit remains.
- P2: 7–8, finishes.
- P1: 8–9, finishes.

### Round Robin Gantt chart (q = 2)

P10–2

P22–4

P34–5

P15–7

P27–8

P18–9

| Process | AT | BT | CT | TAT  | WT   |
| ------- | -- | -- | -- | ---- | ---- |
| P1      | 0  | 5  | 9  | 9    | 4    |
| P2      | 0  | 3  | 8  | 8    | 5    |
| P3      | 0  | 1  | 5  | 5    | 4    |
| Average |    |    |    | 7.33 | 4.33 |

Important: A very small quantum increases context-switch overhead. A very large quantum makes Round Robin behave more like FCFS.

### 2.7.5 Priority Scheduling

Priority scheduling selects a ready process based on its assigned priority.

Priority scheduling can be either preemptive or non-preemptive. In this example, use non-preemptive priority scheduling, where a smaller priority number means a higher priority.

Dataset:

| Process | AT | BT | Priority |
| ------- | -- | -- | -------- |
| P1      | 0  | 5  | 2        |
| P2      | 0  | 3  | 1        |
| P3      | 0  | 1  | 3        |

The order is P2, P1, P3 because P2 has the highest priority, followed by P1 and P3.

### Priority Gantt chart

P20–3

P13–8

P38–9

| Process | AT | BT | Priority | CT | TAT  | WT   |
| ------- | -- | -- | -------- | -- | ---- | ---- |
| P1      | 0  | 5  | 2        | 8  | 8    | 3    |
| P2      | 0  | 3  | 1        | 3  | 3    | 0    |
| P3      | 0  | 1  | 3        | 9  | 9    | 8    |
| Average |    |    |          |    | 6.67 | 3.67 |

Limitation: Low-priority processes may suffer starvation. A technique called aging gradually increases a waiting process's priority to help prevent indefinite postponement.

## Quick comparison of CPU scheduling algorithms

| Algorithm   | Preemptive? | Selection rule          | Main drawback                        |
| ----------- | ----------- | ----------------------- | ------------------------------------ |
| FCFS        | No          | Earliest arrival        | Convoy effect                        |
| SJF         | No          | Shortest burst          | Starvation; burst estimation         |
| SRTF        | Yes         | Shortest remaining time | Starvation; more overhead            |
| Round Robin | Yes         | Fixed time quantum      | Quantum selection overhead           |
| Priority    | Either      | Highest priority        | Starvation of low-priority processes |

## Practice questions

1\. What is a process?

A program stored on disk

A program in execution

A type of hardware

2\. Which scheduler selects a process for the CPU?

Long-term scheduler

Medium-term scheduler

Short-term scheduler

3\. Which algorithm uses a time quantum?

FCFS

Round Robin

SJF

4\. Which algorithm is the preemptive version of SJF?

SRTF

FCFS

Non-preemptive Priority

5\. If CT = 15 and AT = 4, what is TAT?

11

19

15

6\. Which scheduling algorithm can cause the convoy effect?

FCFS

Round Robin

SRTF

Check answers

## Important exam questions

1. Define a process and explain its five states.
2. Differentiate between a process and a thread.
3. Explain CPU-bound and I/O-bound processes with examples.
4. Explain the short-term, medium-term, and long-term schedulers.
5. Differentiate between preemptive and non-preemptive scheduling.
6. Explain FCFS, SJF, SRTF, Round Robin, and Priority Scheduling.
7. Define arrival time, burst time, completion time, turnaround time, waiting time, and response time.
8. Calculate average waiting time and turnaround time using a Gantt chart.
9. What is starvation? How does aging help prevent it?
10. Explain the role of the dispatcher and context switching.

Recommended study order: Process states → PCB and threads → schedulers → scheduling formulas → FCFS → SJF → SRTF → Round Robin → Priority Scheduling.
