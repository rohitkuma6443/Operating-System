# Chapter 1: Introduction to Operating Systems

These notes follow the supplied syllabus. They use simple language, examples, and diagrams written in Markdown so they can be viewed on GitHub, in VS Code, or in a Markdown editor.

## Chapter Contents

- [2.0 Objectives](#20-objectives)
- [2.1 Introduction](#21-introduction-to-operating-systems)
- [2.2 Need for Operating Systems](#22-need-for-operating-systems)
- [2.3 Evolution of Operating Systems](#23-evolution-of-operating-systems)
- [2.4 Operating Systems Architecture](#24-operating-systems-architecture)
  - [2.4.1 Layered Architecture](#241-layered-architecture)
  - [2.4.2 Logical Structure](#242-logical-structure)
- [2.5 Services of Operating Systems](#25-services-of-operating-systems)
- [2.6 Types of Operating Systems](#26-types-of-operating-systems)
- [2.7 Introduction to UNIX](#27-introduction-to-unix-operating-systems)
- [Revision Questions](#revision-questions)

---

## 2.0 Objectives

After completing this chapter, students should be able to:

- Define an Operating System (OS).
- Explain why an operating system is required.
- Describe the evolution of operating systems.
- Explain operating system architecture.
- Describe layered architecture and logical structure.
- Identify the major services provided by an OS.
- Explain different types of operating systems.
- Understand basic UNIX features and commands.

---

## 2.1 Introduction to Operating Systems

### What is an Operating System?

An **Operating System (OS)** is system software that manages computer hardware and software resources and provides an environment in which application programs can run.

In simple words, an operating system acts as a bridge between the user, applications, and computer hardware.

**Examples:** Microsoft Windows, Linux, macOS, Android, iOS, and UNIX.

### Operating System Examples

For operating-system screenshots and official product information, see:
- [Windows](https://www.microsoft.com/windows)
- [Ubuntu Linux](https://ubuntu.com/desktop)
- [Android](https://www.android.com/)
- [Apple macOS](https://www.apple.com/macos/)

### How Does an Operating System Work?

When you open a web browser, play music, or save a file, the operating system coordinates the required operations.

1. The user gives a command, such as opening a browser.
2. The application requests resources from the operating system.
3. The OS manages CPU time, memory, and other resources.
4. The hardware performs the required operations.
5. The result is presented to the user.

### Basic Computer System Diagram

```text
+--------------------------+
|           User           |
+--------------------------+
             |
             v
+--------------------------+
|    Application Software  |
|  Browser, Word, Excel    |
+--------------------------+
             |
             v
+--------------------------+
|     Operating System     |
| Manages system resources |
+--------------------------+
             |
             v
+--------------------------+
|       Hardware           |
| CPU, RAM, Disk, Keyboard  |
+--------------------------+
```

### Main Components of a Computer System

| Component | Meaning | Example |
|---|---|---|
| Hardware | Physical parts of a computer | CPU, RAM, keyboard |
| Operating system | Manages resources and provides services | Windows, Linux |
| Application software | Performs user-oriented tasks | Excel, Chrome |
| User | Person who uses the system | Student, teacher |

### Main Functions of an Operating System

1. **Process management:** Controls running programs and allocates CPU time.
2. **Memory management:** Allocates and releases RAM for programs.
3. **File management:** Creates, stores, organizes, and deletes files.
4. **Device management:** Coordinates devices such as printers, keyboards, and disks.
5. **Security management:** Controls access to files, applications, and system resources.
6. **User interface:** Allows interaction through a Graphical User Interface (GUI) or Command-Line Interface (CLI).

**Example:** When you open Excel, type data, and save a workbook, the OS helps run Excel, allocate memory, accept keyboard input, and store the file on disk.

---

## 2.2 Need for Operating Systems

A computer contains hardware such as the CPU, RAM, storage devices, keyboard, and monitor. Hardware alone does not provide a convenient environment for running applications.

An operating system manages these resources and coordinates the activities of different programs.

### Why Do We Need an OS?

1. **Process management:** Manages running programs and decides how CPU time is shared.  
   *Example:* Running Chrome and Excel at the same time.

2. **Memory management:** Allocates RAM to programs and releases it when appropriate.  
   *Example:* Allocating memory when you open a video editor.

3. **File management:** Helps create, rename, copy, move, and delete files.  
   *Example:* Saving an Excel workbook inside a folder.

4. **Device management:** Coordinates communication with hardware devices, often using device drivers.  
   *Example:* Sending a document to a printer.

5. **Security and access control:** Manages user accounts, permissions, and access to protected resources.  
   *Example:* Preventing a standard user from modifying protected system files.

6. **User interface:** Provides a convenient way to interact with the computer.  
   *Example:* Using the Windows desktop or a Linux terminal.

### What Happens Without an Operating System?

- Users would not have the usual convenient way to run applications.
- Programs would need more direct hardware management.
- File storage and device usage would be more difficult.
- Managing multiple programs and protecting resources would be harder.

**Remember:** An operating system makes computer resources easier to use, share, and manage.

---

## 2.3 Evolution of Operating Systems

Operating systems have developed over time to improve speed, convenience, resource utilization, and the ability to execute multiple tasks.

### 1. Serial Processing (Early Computers)

Early computers generally had no modern operating system. Users or operators loaded and executed jobs one at a time.

**Example:** An operator manually prepared a program for execution.

### 2. Batch Operating Systems

Similar jobs were collected into batches and executed with little direct interaction during execution.

**Example:** Processing thousands of salary records together.

### 3. Multiprogramming Systems

Several jobs could be kept in memory. When one job waited for input/output, the CPU could work on another job.

**Main purpose:** Improve CPU utilization.

### 4. Time-Sharing Systems

CPU time was shared among multiple interactive users or sessions, allowing users to work with the computer responsively.

**Example:** Multiple users working through terminals connected to a shared computer.

### 5. Personal Computer Operating Systems

Operating systems became widely available for individual computers. Early systems often used command-line interfaces; graphical interfaces later became common.

**Examples:** MS-DOS and Microsoft Windows.

### 6. Modern Operating Systems

Modern systems support multitasking, networking, security, graphical interfaces, and complex applications.

**Examples:** Windows, Linux, and macOS.

### 7. Mobile and Cloud-Era Systems

Operating systems support smartphones, tablets, virtual machines, and cloud computing infrastructure.

**Examples:** Android, iOS, and Linux-based cloud servers.

### Evolution Summary

| Stage | Main feature |
|---|---|
| Serial processing | One job at a time, with manual operation |
| Batch processing | Jobs processed in groups |
| Multiprogramming | Several jobs kept ready in memory |
| Time-sharing | Interactive access for multiple users |
| Personal computer OS | Convenient computing for individuals |
| Modern OS | Networking, security, multitasking, and mobile support |

**Important distinction:** Multiprogramming keeps multiple jobs available to use the CPU efficiently. Multitasking lets a system switch among tasks to provide responsive execution. Time-sharing extends interactive resource sharing to multiple users or sessions.

---

## 2.4 Operating Systems Architecture

Operating system architecture describes how the components of an OS are organized and how they communicate.

Common components include:

- **User interface:** Allows users to interact with the system.
- **System calls:** Provide a controlled way for programs to request OS services.
- **Kernel:** The core component that manages CPU scheduling, memory, devices, and other resources.
- **Device drivers:** Help the OS communicate with specific hardware.
- **Hardware:** CPU, RAM, storage, and input/output devices.

### General Architecture Diagram

```text
+-----------------------------+
|       User / Applications   |
+-----------------------------+
              |
              v
+-----------------------------+
| User Interface / System APIs|
+-----------------------------+
              |
              v
+-----------------------------+
|            Kernel           |
| Process, Memory, File, I/O  |
+-----------------------------+
              |
              v
+-----------------------------+
|           Hardware          |
| CPU, RAM, Storage, Devices  |
+-----------------------------+
```

### 2.4.1 Layered Architecture

In a layered architecture, the operating system is organized into layers. Each layer has specific responsibilities and uses services provided by lower layers.

### Example of Layered Architecture

```text
+----------------------------------+
| Layer 4: User Applications       |
| Browser, Text Editor, Spreadsheet|
+----------------------------------+
                  |
                  v
+----------------------------------+
| Layer 3: User Interface/Services |
| Shell, System Call Interface     |
+----------------------------------+
                  |
                  v
+----------------------------------+
| Layer 2: Kernel                  |
| Process, Memory, File, Device Mgmt|
+----------------------------------+
                  |
                  v
+----------------------------------+
| Layer 1: Hardware                |
| CPU, RAM, SSD, Keyboard          |
+----------------------------------+
```

*Note: This is a simplified teaching diagram. Actual operating systems may use different structures and may not follow strict layers.*

### How Does It Work?

Suppose you save a document:

1. You click **Save** in an application.
2. The application requests a file operation.
3. The OS checks permissions and handles the request.
4. The file system and device drivers coordinate with storage hardware.
5. The application receives the result.

### Advantages

- Easier to understand and organize.
- Easier to test and debug individual layers.
- Changes in one layer can sometimes be made without changing others.
- Responsibilities are clearly separated.

### Disadvantages

- Passing through layers can add overhead.
- Designing suitable boundaries between layers can be difficult.
- Strict layering may limit some direct communication needed for performance.

---

### 2.4.2 Logical Structure

The logical structure describes the main functional components of an operating system and how they work together.

### Logical Structure Diagram

```text
+-------------------------------+
| User Interface (GUI or CLI)   |
+-------------------------------+
                |
                v
+-------------------------------+
| System Call Interface         |
+-------------------------------+
                |
                v
+----------------------+----------------------+
| Process Management   | Memory Management     |
+----------------------+----------------------+
| File Management      | Device Management     |
+----------------------+----------------------+
                |
                v
+-------------------------------+
| Hardware                      |
| CPU, RAM, Storage, Devices    |
+-------------------------------+
```

### Main Components

| Component | Responsibility |
|---|---|
| User interface | Accepts user commands |
| System call interface | Allows programs to request OS services |
| Process manager | Schedules and manages processes |
| Memory manager | Allocates and manages memory |
| File system | Organizes files and directories |
| Device management | Coordinates input/output devices |
| Kernel | Provides core OS functionality and controls access to resources |

### Layered Architecture vs Logical Structure

- **Layered architecture** focuses on arranging components into levels.
- **Logical structure** focuses on the roles of components and how they interact.

These concepts overlap, but they are not identical.

---

## 2.5 Services of Operating Systems

An operating system provides services that help users and application programs work efficiently.

### 1. User Interface

Provides ways for users to interact with the computer.

- **GUI:** Graphical User Interface, using windows, icons, and menus.
- **CLI:** Command-Line Interface, using text commands.

*Example:* Windows desktop or a Linux terminal.

### 2. Program Execution

Loads programs into memory and manages their execution.

*Example:* Starting Microsoft Word.

### 3. Input/Output Operations

Coordinates reading and writing through devices.

*Example:* Reading keyboard input or printing a document.

### 4. File-System Management

Creates, reads, writes, renames, and deletes files and directories, subject to permissions.

*Example:* Saving a file as `Report.docx`.

### 5. Process Management

Creates, schedules, coordinates, and terminates processes.

*Example:* Running a browser and a music player together.

### 6. Memory Management

Tracks memory usage and allocates memory to programs.

*Example:* Giving a running application the RAM it needs.

### 7. Communication

Supports communication between processes and across networked computers.

*Example:* A browser communicating with a web server.

### 8. Error Detection

Detects and responds to problems involving hardware, memory, devices, or programs.

*Example:* Reporting that a USB drive cannot be accessed.

### 9. Resource Allocation

Distributes CPU time, memory, storage access, and other resources among competing programs and users.

*Example:* Scheduling CPU time for multiple applications.

### 10. Protection and Security

Enforces permissions and helps prevent unauthorized access.

*Example:* Requiring administrator permission to change protected system settings.

### Practical Example: Printing a Document

```text
1. User clicks Print
         |
         v
2. Application sends print request
         |
         v
3. OS checks permissions and prepares job
         |
         v
4. Printer driver communicates with printer
         |
         v
5. Printer produces the document
```

Several OS services work together in this example, including the user interface, program execution, security, resource management, and input/output management.

---

## 2.6 Types of Operating Systems

Operating systems can be classified by how they process jobs, share resources, handle timing, and support users.

### 1. Batch Operating System

A batch OS processes groups of jobs with little or no user interaction during execution.

**Example:** Payroll processing, billing, and bulk report generation.

**Advantages**
- Suitable for repetitive, large workloads.
- Reduces the need for continuous user interaction.

**Disadvantages**
- Results may not be available immediately.
- Errors can be difficult to identify during execution.

### 2. Multiprogramming Operating System

Keeps several jobs in memory so the CPU can execute another job when the current job is waiting for input/output.

**Example:** Mainframe workloads.

**Advantage:** Improves CPU utilization.

**Disadvantage:** Requires careful memory and CPU scheduling.

### 3. Multitasking Operating System

Allows a user to run or switch between multiple tasks, sharing CPU time as needed.

**Example:** Listening to music while browsing the internet and editing a document.

**Advantage:** Supports convenient use of multiple applications.

**Disadvantage:** Too many resource-intensive tasks can slow the system.

### 4. Time-Sharing Operating System

Shares processing time among multiple users or interactive sessions to provide responsive access.

**Example:** A multiuser UNIX server.

**Advantage:** Many users can use shared computing resources.

**Disadvantage:** Performance may decrease when resources are heavily loaded.

### 5. Multiprocessing Operating System

Supports two or more processors or CPU cores working on tasks concurrently.

**Example:** A modern Linux or Windows system using multiple CPU cores.

**Advantage:** Can improve performance and parallel processing.

**Disadvantage:** Requires coordination of processes and shared resources.

### 6. Real-Time Operating System (RTOS)

Designed to respond to events within specified timing constraints.

- **Hard real-time:** Missing a deadline is unacceptable or can cause system failure.
- **Soft real-time:** Missing a deadline occasionally is undesirable but may be tolerated.

**Examples:** Industrial controllers, medical equipment, and vehicle control systems.

**Advantage:** Predictable response times.

**Disadvantage:** Designing and verifying timing guarantees can be complex.

### 7. Distributed Operating System

Coordinates resources across multiple connected computers and may present them as a unified system.

**Use case:** Distributed computing environments that coordinate processing across several machines.

**Advantage:** Sharing resources and distributing work.

**Disadvantage:** Network failures and coordination add complexity.

### 8. Network Operating System

Provides services to computers connected through a network, such as shared files, authentication, and printer access.

**Examples:** Windows Server and Linux server systems.

**Advantage:** Centralized administration and resource sharing.

**Disadvantage:** Some services depend on network availability.

### 9. Embedded Operating System

Designed for devices with specific functions and often limited hardware resources.

**Examples:** Routers, smart devices, and industrial equipment.

**Advantage:** Designed for the requirements of a particular device.

**Disadvantage:** May have limited memory, storage, or computing capacity.

### 10. Mobile Operating System

Designed for smartphones and tablets, with support for touchscreens, wireless communication, power management, and mobile applications.

**Examples:** Android and iOS.

**Advantage:** Designed for portable, battery-powered devices.

**Disadvantage:** Resources, permissions, and background activity may be restricted.

### Comparison of Operating System Types

| Type | Main purpose | Example or use case |
|---|---|---|
| Batch | Process groups of jobs | Payroll processing |
| Multiprogramming | Improve CPU utilization | Mainframe workloads |
| Multitasking | Run multiple tasks | Desktop computer |
| Time-sharing | Support interactive sessions | Multiuser server |
| Multiprocessing | Use multiple processors or cores | Modern computer |
| Real-time | Meet timing requirements | Industrial controller |
| Distributed | Coordinate multiple computers | Distributed computing |
| Network | Provide network services | File and authentication server |
| Embedded | Control a dedicated device | Router |
| Mobile | Support mobile devices | Android, iOS |

**Exam tip:** Multitasking, multiprocessing, and multiprogramming are different concepts. A system may support more than one of them at the same time.

---

## 2.7 Introduction to UNIX Operating Systems

### What is UNIX?

UNIX is a family of operating systems originally developed at AT&T Bell Labs during the late 1960s and early 1970s. It influenced many modern operating systems and remains important in computing education, servers, and system administration.

UNIX is known for multiuser operation, multitasking, portability, and command-line tools.

### Features of UNIX

1. **Multiuser:** Supports multiple user accounts and sessions.
2. **Multitasking:** Supports the execution of multiple tasks.
3. **Portability:** UNIX was designed to be portable across different hardware platforms.
4. **Security:** Uses user accounts, permissions, and ownership controls.
5. **Hierarchical file system:** Organizes files and directories in a tree structure.
6. **Shell:** Provides a command interpreter for interacting with the system.
7. **Utilities:** Includes tools for working with files, text, processes, and system resources.

### UNIX Architecture

A simplified UNIX architecture consists of users and applications, the shell and utilities, the kernel, and hardware.

```text
+--------------------------------+
| Users and Applications         |
+--------------------------------+
                |
                v
+--------------------------------+
| Shell and Utilities            |
| sh, bash, ls, grep, editors    |
+--------------------------------+
                |
                v
+--------------------------------+
| Kernel                         |
| Process, Memory, File, Devices |
+--------------------------------+
                |
                v
+--------------------------------+
| Hardware                       |
| CPU, RAM, Storage, Peripherals |
+--------------------------------+
```

### 1. Hardware

The physical components of the computer, including CPU, RAM, storage, and peripheral devices.

### 2. Kernel

The core of UNIX. It manages processes, memory, files, devices, and system resources.

### 3. Shell

The shell interprets commands and provides an interface between the user and OS services.

**Examples:** `sh`, `bash`, `ksh`, and `csh`.

### 4. Utilities and Applications

Programs that perform tasks such as listing files, searching text, editing documents, and compiling code.

**Examples:** `ls`, `cp`, `grep`, and text editors.

### Basic UNIX Commands

These commands are commonly used in UNIX-like systems such as Linux and macOS terminals. Some commands and options vary between implementations.

| Command | Purpose | Example |
|---|---|---|
| `pwd` | Display current directory | `pwd` |
| `ls` | List files and directories | `ls` |
| `cd` | Change directory | `cd Documents` |
| `mkdir` | Create a directory | `mkdir Student` |
| `touch` | Create an empty file on common UNIX-like systems | `touch notes.txt` |
| `cp` | Copy a file | `cp a.txt b.txt` |
| `mv` | Move or rename a file | `mv a.txt notes.txt` |
| `rm` | Remove a file | `rm notes.txt` |
| `cat` | Display file contents | `cat notes.txt` |
| `whoami` | Display current username | `whoami` |
| `date` | Display the date and time | `date` |
| `clear` | Clear the terminal screen | `clear` |

### Practical UNIX Example

Suppose you want to create a folder and a file for your class notes.

```bash
mkdir OS_Notes
cd OS_Notes
touch chapter1.txt
ls
pwd
```

**Explanation:**

1. `mkdir OS_Notes` creates a folder.
2. `cd OS_Notes` enters that folder.
3. `touch chapter1.txt` creates an empty file if it does not already exist.
4. `ls` displays the directory contents.
5. `pwd` displays the current directory path.

Expected listing from `ls`:

```text
chapter1.txt
```

**Safety note:** Commands such as `rm` can permanently delete files. Check the target path before running a deletion command.

---

## Revision Questions

### Short-Answer Questions

1. What is an operating system?
2. State four functions of an operating system.
3. What is a batch operating system?
4. What is the kernel?
5. Explain layered architecture.
6. What is the difference between GUI and CLI?
7. What is a real-time operating system?
8. What is UNIX?
9. What does the UNIX shell do?
10. Differentiate between multitasking and multiprocessing.

### Answers

1. **Operating system:** System software that manages computer resources and provides services for applications and users.
2. **Four functions:** Process management, memory management, file management, and device management.
3. **Batch OS:** An OS that processes a group of jobs in batches with little or no user interaction during execution.
4. **Kernel:** The core component of an OS that manages resources and provides essential system services.
5. **Layered architecture:** An arrangement in which OS components are organized into layers with defined responsibilities.
6. **GUI vs CLI:** GUI uses graphical elements such as windows and icons; CLI accepts text-based commands.
7. **Real-time OS:** An OS designed to respond within defined timing constraints.
8. **UNIX:** A family of operating systems originally developed at Bell Labs, known for multiuser operation, multitasking, and command-line tools.
9. **Shell:** Interprets user commands and provides an interface for accessing system services.
10. **Multitasking vs multiprocessing:** Multitasking allows multiple tasks to share CPU time; multiprocessing uses multiple processors or CPU cores to execute work concurrently.

---

## Chapter Summary

- An operating system manages hardware and software resources.
- The OS provides process, memory, file, device, and security management.
- Operating systems evolved from manual serial processing to batch, multiprogramming, time-sharing, personal computer, and modern systems.
- Layered architecture organizes components into levels.
- Logical structure explains the functions and interactions of OS components.
- OS services support program execution, input/output, files, communication, error detection, and security.
- Common OS types include batch, multiprogramming, multitasking, time-sharing, multiprocessing, real-time, distributed, network, embedded, and mobile systems.
- UNIX provides a kernel, shell, utilities, and a hierarchical file system.

## Further Reading

- [OpenStax — What Is an Operating System?](https://openstax.org/books/introduction-computer-science/pages/6-1-what-is-an-operating-system)
- [OpenStax — Fundamental OS Concepts](https://openstax.org/books/introduction-computer-science/pages/6-2-fundamental-os-concepts)
- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/)
- [Ubuntu Desktop](https://ubuntu.com/desktop)
