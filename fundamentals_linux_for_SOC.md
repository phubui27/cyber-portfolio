# Linux Fundamentals for SOC Analysts

## Purpose
This document summarizes the Linux fundamentals I have learned, rewritten from a **Security Operations Center (SOC) perspective**.  
The focus is on understanding Linux as an environment where logs, processes, users, and system activities can be monitored and analyzed for security purposes.

---
## WEEK 1

---

## 1. Linux ecosystem overview

- Linux is an open-source operating system derived from UNIX principles.
- It is developed and maintained by a global community under the Linux Foundation.
- Linux is widely used in servers, cloud infrastructure, and security appliances.

SOC relevance:
- Most enterprise servers, security tools, and logging systems run on Linux.
- Understanding Linux fundamentals is essential for log analysis and incident investigation.

---

## 2. Linux distributions

There are three major Linux distribution families:
- **Red Hat family** (RHEL, CentOS, Rocky Linux)
- **Debian family** (Debian, Ubuntu)
- **SUSE family** (openSUSE, SUSE Linux Enterprise)

SOC relevance:
- SOC analysts often encounter logs from different Linux distributions.
- Core concepts are shared across all families.

---

## 3. Core Linux concepts

- Linux is a **multi-user** and **multi-tasking** operating system.
- Many system features are accessed through files or file-like objects.
- Linux uses background services known as **daemons**.
- A Linux system consists of the kernel plus tools for file, user, and package management.

SOC relevance:
- Multiple users and services mean multiple potential attack surfaces.
- Daemons generate logs that SOC analysts must monitor.

---

## 4. Disk, partitions, and boot process

- A disk can be divided into multiple **partitions**.
- A **filesystem** defines how data is stored and retrieved.
- Linux boot process:
  - BIOS/UEFI
  - Bootloader
  - Kernel
  - initramfs
  - init system

SOC relevance:
- Understanding the boot process helps during incident response and system recovery.
- Separate partitions can limit damage during system compromise.

---

## 5. Desktop environment (GNOME) – overview only

- GNOME is a common Linux desktop environment.
- It provides a graphical login manager (gdm) and user session management.
- Each user has a home directory.

SOC note:
- Desktop themes and UI customization were covered but are **not directly relevant** to SOC daily work.
- Session login and logout concepts are relevant for understanding user activity.

---

## 6. System configuration and time management

- Linux internally uses **UTC** for timekeeping.
- Time synchronization is commonly handled via **NTP**.
- Network Manager manages wired, wireless, and VPN connections.

SOC relevance:
- Accurate system time is critical for log correlation across systems.
- Network configuration affects visibility and detection of suspicious connections.

---

## 7. Package management

- Debian-based systems use **dpkg** and **apt**.
- Red Hat-based systems use **RPM** and tools like **dnf**.
- openSUSE uses **zypper**.

SOC relevance:
- Package managers are used to install and update software.
- Unexpected package installations may indicate compromise or misconfiguration.

---

## 8. Linux terminal and filesystem navigation

- Linux supports virtual terminals and terminal emulators.
- Users can log in locally or remotely.
- Two types of paths:
  - **Absolute paths**
  - **Relative paths**

Key commands:
- `pwd`, `ls`, `cd` for navigation
- `cd -` to return to the previous directory

SOC relevance:
- SOC analysts rely on the terminal to locate and access log files quickly.

---

## 9. File search and file handling

- `locate` performs database-based file searches.
- `find` searches directories recursively and can execute commands with `-exec`.
- Hard and symbolic links allow flexible file referencing.
- `touch` creates files or updates timestamps.

SOC relevance:
- Useful for locating logs, scripts, or suspicious files.
- File timestamps are important during investigations.

---

## 10. Linux documentation and help systems

- Linux documentation sources include:
  - `man` pages
  - `info`
  - `--help` or `-h`
  - Online documentation

SOC relevance:
- SOC analysts must quickly reference command usage during investigations.
- Efficient use of documentation saves time under pressure.

---

## 11. Processes and system activity

- Processes execute tasks on the system and are identified by **PID**.
- Processes can be interactive or non-interactive.
- Process priority can be adjusted using **nice** values.

Key commands:
- `ps` to view running processes
- `top` for real-time system and process monitoring

SOC relevance:
- Unusual or resource-heavy processes may indicate malware or abuse.
- Process monitoring is essential during incident response.

---

## 12. Job scheduling

- Linux supports background and foreground jobs.
- `at` schedules one-time tasks.
- `cron` schedules recurring tasks.

SOC relevance:
- Attackers may use cron jobs for persistence.
- SOC analysts must inspect scheduled tasks during investigations.

---

## 13. Applications overview (high-level only)

- Linux supports many applications:
  - Web browsers
  - Email clients
  - Office suites
  - Multimedia and graphics tools

SOC note:
- These applications were covered at a high level.
- They are **not the focus** of SOC operations but provide context for user activity.

---

## Key takeaways

- Linux is a core environment for SOC analysts.
- Logs, processes, users, and scheduled tasks are primary investigation targets.
- Understanding Linux fundamentals enables effective log analysis and incident response.
- The goal is not system administration, but **security visibility and detection**.
