# Cybersecurity Homelab

## Overview

This project documents the physical cybersecurity homelab I built using repurposed Dell OptiPlex computers.

The purpose of the lab is to create a realistic environment where I can practice networking, system administration, virtualization, Active Directory, Linux, firewall configuration, security monitoring, and offensive and defensive cybersecurity techniques.

Instead of running the entire lab from a single computer, I assigned different physical systems specific roles and use Proxmox to host several virtual machines. I also built a dedicated lab network using pfSense as the firewall and router, along with an 8-port Ethernet switch to provide wired connectivity between the physical systems.

This homelab serves as the foundation for my pfSense network security, SIEM and Active Directory, and Wazuh detection engineering projects.

## Physical Hardware

The lab is built using several Dell OptiPlex systems that were repurposed from my workplace.

I upgraded some of the systems with additional RAM and storage so they could better support virtualization and security tools.

### Dell OptiPlex 3050

**Operating System:** Windows 11
**Role:** Management Workstation

This is my primary computer for managing and accessing the rest of the homelab.

I use this system to:

* Access the Proxmox web interface
* Manage virtual machines
* Connect to the physical Kali Linux workstation using SSH for remote security testing
* Access Wazuh
* Configure pfSense
* Administer Windows Server and Active Directory
* Perform general lab management and troubleshooting

### Dell OptiPlex 9010

**Platform:** Proxmox VE
**Role:** Virtualization Host

The OptiPlex 9010 runs Proxmox and hosts the majority of the virtual machines used in the lab.

Virtual machines currently running on this system include:

* Windows Server 2022
* Windows 10
* Ubuntu Server
* Ubuntu Desktop
* Metasploitable 2

Proxmox allows me to manage multiple operating systems from one physical server while learning virtualization, resource allocation, virtual networking, and system administration.

### Dell OptiPlex 3040

**Platform:** pfSense
**Role:** Firewall and Router

The OptiPlex 3040 is dedicated to running pfSense and serves as the primary firewall and router for my cybersecurity homelab.

Rather than relying solely on my existing home router to manage the lab network, I use pfSense to route and control traffic for the lab environment.

During the build, I initially purchased an inexpensive network interface card that was not compatible with pfSense. After troubleshooting the issue and researching hardware compatibility, I purchased replacement NICs that were properly supported and successfully completed the firewall and router configuration.

This system is used for:

* Routing network traffic
* Firewall configuration
* Network segmentation
* Traffic filtering
* Firewall rules
* Network aliases
* SSH access restrictions
* Network monitoring

### Dell OptiPlex 3060

**Operating System:** Kali Linux
**Role:** Security Testing Workstation

Kali Linux runs directly on the OptiPlex 3060 as a physical security testing system.

Rather than operating Kali locally each time I perform testing, I can remotely access the system from my Windows 11 management workstation using SSH.

I use Kali to perform controlled security testing against systems in the homelab.

Activities include:

* Nmap scanning
* Network reconnaissance
* Port and service discovery
* Connectivity testing
* Metasploit testing
* Controlled exploitation of Metasploitable 2
* Generating activity for firewall and SIEM analysis

## Network Infrastructure

The homelab uses a dedicated 8-port Ethernet switch to provide wired network connectivity between the physical systems.

The switch connects the lab systems to the Dell OptiPlex 3040 running pfSense, which acts as the firewall and router for the lab network.

The physical network consists of:

* **Dell OptiPlex 3040** — pfSense firewall and router
* **8-port Ethernet switch** — Provides wired connectivity between the lab systems
* **Dell OptiPlex 3050** — Windows 11 management workstation
* **Dell OptiPlex 9010** — Proxmox virtualization server
* **Dell OptiPlex 3060** — Kali Linux security testing workstation

The virtual machines hosted by Proxmox communicate through the Proxmox server's network connection, allowing them to interact with other systems on the lab network.

This setup gives me a dedicated environment where I can configure firewall rules, route traffic, monitor network activity, perform security testing, and observe communication between physical and virtual systems.

## Virtual Machines

The Proxmox server hosts several virtual machines that each serve a specific role within the environment.

### Windows Server 2022

Used for:

* Active Directory Domain Services
* Domain Controller configuration
* User and computer management
* Group Policy
* Windows authentication testing
* Security logging

### Windows 10

Used as a Windows endpoint for:

* Active Directory domain testing
* Sysmon monitoring
* PowerShell logging
* Wazuh agent monitoring
* Security testing
* Authentication analysis

### Ubuntu Server

Used as the Linux server hosting Wazuh.

Configuring this system required me to become more comfortable with Linux server administration and working without a graphical desktop environment.

The server provides the centralized Wazuh infrastructure used to collect and analyze security telemetry generated throughout the lab.

### Ubuntu Desktop

Used as a Linux workstation for:

* Linux administration
* Networking practice
* Connectivity testing
* General lab testing

### Metasploitable 2

Metasploitable 2 is an intentionally vulnerable Linux system used as a controlled target for security testing.

I use the physical Kali Linux workstation to scan and interact with Metasploitable 2 and practice controlled exploitation using Metasploit Framework.

This provides a safe environment for practicing reconnaissance, vulnerability discovery, and exploitation while observing how malicious or suspicious activity appears across the lab network and security monitoring tools.

## Learning SSH

Building the homelab gave me hands-on experience using SSH as part of my security testing workflow.

I used SSH to remotely connect from my Windows 11 management workstation to the physical Kali Linux machine. This allowed me to control Kali remotely and perform security testing against the virtual machines running within the Proxmox environment.

From the Kali system, I used tools such as Nmap to scan the virtual machines, identify active hosts, discover open ports, and examine services running across the lab network.

I also used Kali to launch Metasploit Framework (`msfconsole`) and perform controlled exploitation against the intentionally vulnerable Metasploitable 2 virtual machine.

This workflow gave me practical experience with:

* Remotely accessing Kali Linux using SSH
* Linux command-line navigation
* Running Nmap scans from a remote Kali system
* Identifying hosts, ports, and services
* Using Metasploit Framework (`msfconsole`)
* Testing exploits against Metasploitable 2
* Establishing sessions with a vulnerable target in a controlled environment
* Understanding communication between physical and virtual systems

Using SSH allowed me to perform much of this testing directly from my Windows 11 management workstation while the security tools and attacks were executed from the dedicated physical Kali Linux machine.

## Hardware Upgrades and Troubleshooting

The original computers had limited hardware resources, so I upgraded systems with additional RAM and storage where needed.

I also encountered a hardware compatibility issue while building the pfSense firewall.

The first NIC I purchased was not recognized properly by pfSense. After researching the issue, I determined that the hardware was not properly supported and replaced it with compatible network interface cards.

I also added an 8-port Ethernet switch to the environment so the physical systems could connect to the dedicated pfSense-controlled lab network.

These experiences helped reinforce the importance of:

* Hardware compatibility research
* Driver support
* Troubleshooting
* Network interface configuration
* Physical network design
* Planning hardware around operating system requirements

## Lab Environment

| Platform / Operating System | Role                                 | System                 |
| --------------------------- | ------------------------------------ | ---------------------- |
| Windows 11                  | Management workstation               | Dell OptiPlex 3050     |
| Proxmox VE                  | Virtualization host                  | Dell OptiPlex 9010     |
| pfSense                     | Firewall / Router                    | Dell OptiPlex 3040     |
| Kali Linux                  | Security testing workstation         | Dell OptiPlex 3060     |
| Ethernet                    | Physical network connectivity        | 8-Port Ethernet Switch |
| Windows Server 2022         | Active Directory / Domain Controller | Virtual Machine        |
| Windows 10                  | Windows endpoint                     | Virtual Machine        |
| Ubuntu Server               | Wazuh server                         | Virtual Machine        |
| Ubuntu Desktop              | Linux workstation                    | Virtual Machine        |
| Metasploitable 2            | Vulnerable testing target            | Virtual Machine        |


## Skills Developed

Through building and maintaining this homelab, I have gained hands-on experience with:

* Computer hardware upgrades
* Proxmox virtualization
* Virtual machine management
* Windows Server 2022
* Active Directory
* Windows administration
* Linux administration
* SSH
* pfSense
* Routing
* Firewall configuration
* Network segmentation
* Ethernet switching
* Physical network design
* Network troubleshooting
* Kali Linux
* Nmap
* Metasploit Framework
* Controlled exploitation
* Wazuh
* Sysmon
* SIEM monitoring
* Security testing
* Hardware compatibility troubleshooting

## Related Projects

This homelab provides the infrastructure used for several cybersecurity projects:

* **Network Security / pfSense Lab**
* **SIEM & Active Directory Security Lab**
* **Wazuh Detection Engineering Lab**

These projects build on the same environment and focus on networking, system administration, security monitoring, detection engineering, and attack simulation.

