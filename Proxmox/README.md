# Proxmox Setup
## Updates being made as system changes
This project details the setup and configuration of Proxmox Virtual Environment (VE) as the primary hypervisor for a homelab. Proxmox VE is an open-source server virtualization platform that allows you to manage VMs and containers efficiently, making it ideal for homelab infrastructure.

## Table of Contents
- [Introduction](#introduction)
- [Hardware Requirements](#hardware-requirements)
- [Software Requirements](#software-requirements)
- [Installation](#installation)
- [Post-Installation Configuration](#post-installation-configuration)
- [Networking](#networking)
- [VM and Container Setup](#vm-and-container-setup)
- [Backup and Recovery](#backup-and-recovery)
- [Monitoring and Management](#monitoring-and-management)

## Introduction
Proxmox VE is an excellent choice for creating and managing a home lab due to its ease of use, flexibility, and powerful feature set, including support for both VMs and containers. This guide will walk you through the process of installing and configuring Proxmox VE for your homelab, from hardware setup to managing VMs and containers.

## Hardware Requirements
To run Proxmox VE efficiently, the following hardware is recommended:
- **CPU**: 64-bit processor with Intel VT-x/AMD-V support
- **RAM**: Minimum 4GB, but 16GB or more is recommended for multiple VMs/containers
- **Storage**: SSD or NVMe drive for fast performance, with additional storage for VMs/containers
- **Network**: A reliable Ethernet connection, with optional VLAN support for advanced networking configurations
  
My current setup is as follows:
- **CPU**: Intel i7 8700K 6 Core/12 Threads
- **RAM**: 32GB Corsair Vengence(2x16GB sticks)
- **Storage**: 1x 240GB Kingston SSD(boot) and 2x 12TB Seagate BarraCuda pro running Raid 1 
- **Network**: Onboard 1GB ethernet port (possibly upgrading to 2.5GB NIC)
- **GPU**: Sparkle Intel Arc A310 (Supports AV1)
## Software Requirements
- **Proxmox VE ISO**: Download from the official [Proxmox website](https://www.proxmox.com/en/downloads).
- **Etcher or Rufus**: To create a bootable USB drive from the ISO. **OR** **Ventoy USB** This is the option I used.
- **Web browser**: To access the Proxmox VE web interface.

## Installation
1. **Create a Bootable USB Drive**: Use Etcher or Rufus to flash the Proxmox VE ISO onto a USB drive. **OR** **Ventoy**
   
2. **Boot from USB**: Insert the bootable USB drive into your server and boot from it.

3. **Install Proxmox**: Follow the on-screen instructions to install Proxmox onto your selected storage device.

4. **Access Web Interface**: After installation, access the Proxmox web interface by navigating to `http://<your-server-ip>:8006` in a browser.

## Post-Installation Configuration

**Configure Storage**: Set up local storage or connect to network-attached storage (NAS) for managing your VM/Container data.
- I used ZFS to setup Raid 1(Mirror) on my two data hard drives.
- <img src="/Proxmox/Photos/proxmoxpic2.png" alt="Description" width="500"/>

**Update Proxmox**: Run updates to ensure you have the latest security patches and features:
  
Enable No-Subscription Repository: If you're using the free version, configure the no-subscription repository:
- <img src="/Proxmox/Photos/proxmoxpic1.png" alt="Description" width="500"/>

## Networking
Bridge Configuration: Set up a network bridge to allow VMs and containers to communicate with other devices on your network.
-This has been automatically done when setting up my containers on this machine as well as VMs

VLAN Support: Configure VLANs if you are using multiple network segments for VMs and containers.

## VM and Container Setup
Create a VM: Using the web interface, create a new VM for services such as Jellyfin, Minecraft, or others.

LXC Containers: Use LXC containers for lightweight services such as Pi-hole or Home Assistant.

## Backup and Recovery
Backup Strategy: Set up regular backups of your VMs and containers to avoid data loss. Use Proxmox's built-in backup feature to schedule backups.

Restore: In case of failure, restore your VMs/containers from the backup files.

## Monitoring and Management
Proxmox Web Interface: Use the Proxmox web interface for real-time monitoring of CPU, memory, and disk usage.

Proxmox CLI: Use Proxmox command-line tools for advanced management tasks

Alerts and Notifications: Set up email or webhook alerts for system events or failures.
