## Phase 1: Virtual Machine Setup

### Overview
The goal of Phase 1 was to build the foundation of the home lab by setting 
up a virtualization environment and deploying two virtual machines — Kali 
Linux and Ubuntu Server. This simulates having multiple systems in a network 
environment, which is the baseline for all future lab work.

### Environment
- Host Machine: HP Pavilion x360 (Intel i5-1135G7, 8GB RAM, Windows 11 Home)
- Virtualization Platform: Oracle VirtualBox 7.2
- VM Storage Location: C:\HomeLab (local drive, outside OneDrive)

### Why VirtualBox?
VirtualBox was chosen because it is free and open source, runs natively on 
Windows, and supports pre-built VM images. This made it the most practical 
choice for a home lab on a personal laptop without additional cost.

### Virtual Machines Deployed

#### Kali Linux 2026.2
- **Purpose:** Primary attack and security testing machine. Kali is the 
  industry standard penetration testing distribution and comes pre-loaded 
  with hundreds of security tools out of the box.
- **RAM Allocated:** 2048 MB
- **Storage:** 80GB virtual disk
- **Configuration:** Imported pre-built VirtualBox image from kali.org
- **Post-install steps:**
  - Ran full system update: `sudo apt update && sudo apt upgrade -y`
  - Changed default password from factory default for security hardening

#### Ubuntu Server 26.04 LTS
- **Purpose:** Simulated server environment for practicing Linux 
  administration, networking, and future Active Directory integration.
- **RAM Allocated:** 2048 MB
- **Storage:** 25GB virtual disk
- **Configuration:** Installed from ISO using guided storage layout with LVM
- **Post-install steps:**
  - Ran full system update: `sudo apt update && sudo apt upgrade -y`
  - Confirmed SSH keys were generated on first boot

### Issues Encountered and Resolved

**Issue 1: Missing Visual C++ Redistributable**
VirtualBox 7.2 requires the Microsoft Visual C++ 2019 Redistributable to 
run. The installer failed on first attempt. Resolved by downloading and 
installing the x64 redistributable from Microsoft before re-running the 
VirtualBox installer.

**Issue 2: OneDrive File Locking**
VirtualBox was unable to open the Kali disk image file because it was stored 
inside the OneDrive synced Documents folder. OneDrive locks large files 
during cloud sync which prevents VirtualBox from accessing them. Resolved by 
moving all VM files to C:\HomeLab, a local directory completely outside of 
OneDrive.

**Issue 3: Broken VM Registry Reference**
After moving the files, VirtualBox still had an internal reference pointing 
to the old file location. Resolved by removing the broken VM entry from 
VirtualBox and re-importing the machine directly from the new C:\HomeLab 
location using File > Open.

**Issue 4: Ubuntu Server Boot Order**
Ubuntu Server was booting from the network (PXE) instead of the ISO on 
first start. Resolved by changing the boot order in VirtualBox Settings > 
System to place Optical Drive above Hard Disk, forcing it to boot from the 
ISO first.

### What I Learned
- How virtualization works and how VMs interact with host system resources
- The importance of storing VM files outside of cloud-synced folders
- Basic Linux system administration including package management and 
  password hardening
- How to troubleshoot VirtualBox configuration issues

### Screenshots
![Kali System Update](Screenshot%202026-07-08%20184007.png)
![Kali Password Update](Screenshot%202026-07-08%20184521.png)
![Ubuntu Server Login](GithubUbuntu1.webp)
![Ubuntu Server Update](GithubUbuntu2.webp)

## Phase 2: Active Directory Lab (Coming Soon)
## Phase 3: Splunk SIEM (Coming Soon)
## Phase 4: TryHackMe SOC Level 1 (In Progress)

## Goals
Building practical skills for help desk and SOC analyst roles in the DMV area.
