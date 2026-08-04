# Cybersecurity Home Lab

## Overview
Personal cybersecurity home lab built on an HP Pavilion x360 (Intel i5, 8GB RAM) running VirtualBox. This is an ongoing project where I'm simulating a small enterprise environment to get hands-on practice and build real skills for help desk and SOC analyst roles.

## Environment
- Host Machine: HP Pavilion x360 (Intel i5-1135G7, 8GB RAM, Windows 11 Home)
- Virtualization Platform: Oracle VirtualBox 7.2
- VM Storage Location: C:\HomeLab (local drive, outside OneDrive)

## Why VirtualBox?
I went with VirtualBox because it's free, open source, and runs well on Windows. It also supports pre-built VM images, which made it the easiest option for a home lab on a personal laptop without spending extra money.

---

## Phase 1: Virtual Machine Setup

### Overview
The goal of Phase 1 was to get the foundation of my home lab up and running. That meant setting up a virtualization platform and installing two virtual machines, Kali Linux and Ubuntu Server. This gives me multiple systems to work with like a real network, which everything else in the lab builds on.

### Virtual Machines Deployed

**Kali Linux 2026.2**
- **Purpose:** My main machine for security testing and attacks. Kali is the standard pentesting distro and comes with most of the tools I need already installed.
- **RAM Allocated:** 2048 MB
- **Storage:** 80GB virtual disk
- **Configuration:** Imported the pre-built VirtualBox image straight from kali.org
- **Post-install steps:**
  - Updated the system with `sudo apt update && sudo apt upgrade -y`
  - Changed the default password right away for basic security

**Ubuntu Server 26.04 LTS**
- **Purpose:** Simulates a server environment so I can practice Linux administration, networking, and later Active Directory integration.
- **RAM Allocated:** 2048 MB
- **Storage:** 25GB virtual disk
- **Configuration:** Installed from the ISO using the guided storage layout with LVM
- **Post-install steps:**
  - Updated the system with `sudo apt update && sudo apt upgrade -y`
  - Confirmed SSH keys got generated on first boot

### Issues Encountered and Resolved

**Issue 1: Missing Visual C++ Redistributable**
VirtualBox 7.2 needs the Microsoft Visual C++ 2019 Redistributable to run, and the installer failed the first time I tried. I fixed it by downloading and installing the x64 redistributable from Microsoft, then running the VirtualBox installer again.

**Issue 2: OneDrive File Locking**
VirtualBox couldn't open the Kali disk image because it was sitting inside my OneDrive synced Documents folder. OneDrive locks large files while syncing, which blocked VirtualBox from accessing them. I fixed this by moving all my VM files to C:\HomeLab, which is completely outside OneDrive.

**Issue 3: Broken VM Registry Reference**
After moving the files, VirtualBox was still pointing to the old file location. I removed the broken VM entry and re-imported it straight from the new C:\HomeLab location using File > Open.

**Issue 4: Ubuntu Server Boot Order**
Ubuntu Server tried to boot from the network instead of the ISO on the first attempt. I fixed this in VirtualBox Settings under System by moving the Optical Drive above the Hard Disk in the boot order, so it boots from the ISO first.

### What I Learned
- How virtualization works and how VMs use the host system's resources
- Why it matters to keep VM files outside of cloud synced folders
- Basic Linux administration, including package management and password hardening
- How to troubleshoot common VirtualBox configuration problems

### Screenshots
![Kali System Update](Screenshot%202026-07-08%20184007.png)
![Kali Password Update](Screenshot%202026-07-08%20184521.png)
![Ubuntu Server Login](GithubUbuntu1.webp)
![Ubuntu Server Update](GithubUbuntu2.webp)

---

## Phase 2: Active Directory Lab (In Progress)

### Overview
This phase is about building out a Windows Server domain environment, which is one of the most common setups I'll run into in a real help desk or SOC role. I'm installing Windows Server 2022, promoting it to a Domain Controller, and setting up users, groups, and Group Policy from scratch.

### Progress So Far
- Downloaded the Windows Server 2022 Evaluation (free 180 day trial) and created the VM in VirtualBox
- Installed Windows Server 2022
- Renamed the server to DC01

### Issues Encountered and Resolved

**Issue 5: VM Freeze During Restart**
While restarting DC01 after renaming it, the VM froze and stopped responding. I gave it a few minutes in case it was just working slowly, but it never came back on its own. I used VirtualBox's Machine > Reset option to force a reboot, and it came back up fine with no data loss. The rename to DC01 had also saved correctly. This was probably caused by the VM only having 2048 MB of RAM, which can make restarts look frozen when Windows Server is actually still working in the background.

### Still To Do
- Install the Active Directory Domain Services role
- Promote DC01 to a Domain Controller
- Create the domain corp.local
- Create users, groups, and Organizational Units
- Set up Group Policy

---

## Phase 3: Splunk SIEM (Coming Soon)

## Phase 4: TryHackMe SOC Level 1 (In Progress)

## Skills Demonstrated
- Virtualization and VM management
- Linux command line basics
- System hardening
- Windows Server administration

## Goals
Building practical skills for help desk and SOC analyst roles in the DMV region.
