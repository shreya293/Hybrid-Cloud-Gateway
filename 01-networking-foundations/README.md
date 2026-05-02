# Phase 1: Hybrid-Gateway Networking & Core Infrastructure

This repository documents the architectural foundation of a Hybrid-Cloud Gateway. The project establishes a secure, routed bridge between an on-premises Enterprise Lab (Windows Server 2022) and an external Cloud-Exit point (pfSense)[cite: 2].

## 🏗️ Virtual Topology
* **Hypervisor**: VMware Workstation Pro (Isolated LAN Segments)[cite: 2].
* **Gateway**: pfSense 2.8.1-RELEASE (Community Edition)[cite: 2].
* **Directory Services**: Windows Server 2022 (`singh.com` domain)[cite: 2].
* **Internal Client**: Windows 11 Enterprise[cite: 2].

---

## 🛠️ Implementation Modules
*Select a module below to view technical configurations and verification receipts.*

<details>
<summary><b>Module 1: Automated Installation & Environment Detection</b></summary>

The deployment begins with provisioning the pfSense kernel on the hypervisor. This stage focuses on selecting the correct stable build and ensuring the software correctly identifies the virtualized hardware.

**Technical Highlights:**
* **Stable Build**: Deployment of **2.8.1-RELEASE** to ensure compatibility with modern security packages[cite: 2].
* **Hypervisor Handshake**: The system successfully detected the **VMware Virtual Machine** environment, allowing for optimized driver performance.

**Implementation Evidence:**
![Software Version Selection](../assets/pfsense-version.png)
<img src="assets/pfsense-version.png" alt="Ping Test Verification" width="600">

*Figure 1: Selection of the current stable software branch.*

![Hardware Detection](../assets/vmware-detection.png)
*Figure 2: System-level confirmation of the VMware virtual environment.*

</details>

<details>
<summary><b>2. Interface Provisioning (WAN/LAN Logic)</b></summary>

This module documents the "Blue Screen" manual configuration where the physical logic of the gateway is defined. This prevents traffic leakage between the internal lab and the host network.

**Technical Highlights:**
* **WAN Mapping (`le0`)**: Manually assigned to the external virtual adapter for internet transit[cite: 2].
* **LAN Mapping (`le1`)**: Mapped to the private LAN segment to isolate enterprise traffic[cite: 2].
* **Static Gateway**: Assigned `192.168.10.254` as the persistent internal exit point[cite: 2].
* **Console Sovereignty**: Established the primary management menu, allowing for low-level system recovery and IP auditing without a GUI[cite: 2].

**Implementation Evidence:**
![WAN Assignment](../assets/wan-assignment.png)
*Figure 3: Manual provisioning of the external WAN interface.*

![LAN Assignment](../assets/lan-assignment.png)
*Figure 4: Manual provisioning of the internal LAN interface.*

![Console Home Menu](../assets/pfsense-console-menu.png)
*Figure 4: The master console menu showing the final verified IP schema (192.168.10.254).*

</details>

<details>
<summary><b>3. Enterprise Identity & DHCP Integration</b></summary>

In a professional hybrid environment, identity management is centralized. This module documents the handshake between the Windows Domain Controller and the pfSense Gateway.

**Technical Highlights:**
* **Service Offloading**: DHCP management is handled by **Windows Server 2022** for centralized control[cite: 2].
* **Scope Option 003**: Configured the **Router** option to point all `singh.com` assets to the pfSense LAN IP (`.254`)[cite: 2].

**Implementation Evidence:**
![Static LAN Setup](../assets/static-lan-setup.png)
*Figure 5: Manual definition of the static LAN IP via the setup wizard.*

![DHCP Scope Configuration](../assets/dhcp-options.png)
*Figure 6: Windows Server DHCP Manager confirming Scope Option 003 integration[cite: 2].*

</details>

<details>
<summary><b>4. System Audit & Connectivity Validation</b></summary>

The final module proves the integrity of the network stack. It validates that the client machine can successfully navigate from the internal domain to the public internet.

**Technical Highlights:**
* **Dashboard Verification**: Confirmed the gateway is on the latest version with both interfaces active[cite: 2].
* **Routing Audit**: Verified the client workstation successfully inherited the gateway address and DNS suffix[cite: 2].
* **Transit Proof**: 0% packet loss during ICMP stress tests to `8.8.8.8`[cite: 2].

**Implementation Evidence:**
![System Dashboard](../assets/system-dashboard.png)
*Figure 7: Final web dashboard showing the operational state of the gateway[cite: 2].*

![Connectivity Victory](../assets/ping-test.png)
*Figure 8: Successful internet transit from the internal Windows 11 client[cite: 2].*

</details>

---

## 💡 Engineering Resolution
By manually defining the **Interface Assignments** and **DHCP Scope Options**, I resolved a common "Gateway Discovery" issue[cite: 2]. This ensures that the `singh.com` domain is now ready for high-level security implementation in Phase 2.

#Cybersecurity #NetworkEngineering #pfSense #ActiveDirectory #HomeLab #WorldSkills2028
