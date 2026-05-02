# Hybrid Cloud Infrastructure Gateway

## Project Overview
This project demonstrates the design and implementation of a secure hybrid gateway. It establishes a robust foundation for bridging a local enterprise environment (Windows Server 2022) with cloud-ready infrastructure using pfSense.

### Core Objectives
* **Scalable Networking**: Implementation of a dual-interface gateway (WAN/LAN).
* **Enterprise Identity**: Full Active Directory Domain Services (AD DS) integration.
* **Service Management**: Centralized DHCP and DNS management for internal assets.
* **Future Security**: Preparation for IDS/IPS and Cloud Identity Synchronization.

## Lab Topology
* **Gateway**: pfSense (Community Edition)
* **Identity Server**: Windows Server 2022 (`singh.com` domain)
* **Workstation**: Windows 11 Enterprise
* **Virtualization**: VMware Workstation Pro (Isolated LAN Segments)

---
## Navigation
1. [Phase 1: Networking Foundations](./01-networking-foundations/)
2. Phase 2: Security Filtering (Work in Progress)
3. Phase 4: Cloud Identity Sync (Planned)
