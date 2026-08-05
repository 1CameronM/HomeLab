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

## Phase 1: Virtual Machine Setup ✅

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

## Phase 2: Active Directory Lab ✅

### Overview
This phase was about building out a Windows Server domain environment, which is one of the most common setups I'll run into in a real help desk or SOC role. I installed Windows Server 2022, promoted it to a Domain Controller, and set up Organizational Units, users, groups, and Group Policy from scratch.

### What Was Built
- Installed Windows Server 2022 Evaluation and renamed the server to DC01
- Installed the Active Directory Domain Services (AD DS) role
- Promoted DC01 to a Domain Controller, creating the domain corp.local
- Created two Organizational Units: Employees and IT
- Created user accounts: John Smith (IT) and Sarah Johnson (Employees)
- Created a security group called IT Staff and added John Smith as a member
- Created a Group Policy Object called Employee Restrictions and linked it to the Employees OU, configured to prohibit access to Control Panel and PC settings

### Why This Setup
Organizational Units, security groups, and Group Policy are the building blocks of how real companies manage users and computers in Active Directory. Separating Employees from IT mirrors how a real organization would structure permissions, and the Group Policy Object shows how admins push settings out to a whole group of users at once instead of configuring machines one by one.

### Issues Encountered and Resolved

**Issue 5: VM Freeze During Domain Controller Promotion**
The VM froze twice while promoting DC01 to a Domain Controller, both times right after entering the DSRM password and clicking Next. I waited several minutes each time with no change, then used VirtualBox's Machine > Reset to force a reboot. After it happened a second time, I realized the VM was underpowered for this step. I shut the VM down and increased the base memory from 2048 MB to 4096 MB in VirtualBox settings. After the RAM increase, the promotion completed successfully on the next attempt with no freezing.

**Issue 6: VM Freeze During Group Creation**
The VM froze again briefly while creating the IT Staff security group and adding a member. After a Reset, I checked Active Directory Users and Computers and found the group and membership had actually saved correctly before the freeze happened, so no work was lost. This confirmed that these freezes are tied to the VM catching up on background AD DS processes rather than actual crashes.

**Issue 7: Shutdown Event Tracker Popups**
After each forced Reset, Windows Server displayed a Shutdown Event Tracker prompt asking why the computer shut down unexpectedly. This is expected behavior after a hard reset and not an error. I entered a short comment each time (for example, "Lab VM reset during AD DS promotion") and continued.

### What I Learned
- How to install the AD DS role and promote a server to a Domain Controller
- How Organizational Units are used to structure users and computers in a domain
- How to create users and security groups in Active Directory
- How Group Policy Objects are created and linked to specific OUs to apply settings
- That VM freezes during resource-heavy operations like domain promotion are often tied to insufficient RAM, and that increasing allocated memory can resolve the issue entirely
- How to recover safely from a frozen VM using VirtualBox's Reset function without losing configuration work already completed

### Screenshots
![DC01 Domain Confirmed](dc01-domain-confirmed.png)
![Active Directory OUs](ad-ous-created.png)
![IT Staff Group Members](itstaff-group-members.png)
![Group Policy Editor](gpo-control-panel-restriction.png)
## Phase 3: Splunk SIEM (Coming Soon)

## Phase 4: TryHackMe SOC Level 1 (In Progress)

## Skills Demonstrated
- Virtualization and VM management
- Linux command line basics
- System hardening
- Windows Server administration
- Active Directory Domain Services (AD DS)
- Group Policy configuration
- VM troubleshooting and resource management

## Goals
Building practical skills for help desk and SOC analyst roles in the DMV region.
