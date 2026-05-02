# Phase 1: Networking Foundations & Enterprise Integration

This phase documents the successful establishment of the core infrastructure. The primary goal was to bridge an internal Active Directory environment with a secure pfSense gateway to allow controlled external traffic transit.

## 🏗️ Virtual Network Architecture
The environment is hosted on **VMware Workstation Pro** using custom **LAN Segments** to isolate laboratory traffic from the host machine.

* **Gateway (pfSense)**: Managed via a dual-homed configuration (WAN/LAN).
* **Directory Services (Windows Server 2022)**: Hosting the `singh.com` forest and enterprise DHCP/DNS.
* **Endpoint (Windows 11)**: A domain-joined workstation acting as the primary internal node.

---

## 🛠️ Technical Deep-Dive (Configuration Receipts)
*Click the toggles below to explore the specific configurations and manual audits performed in this phase.*

<details>
<summary><b>1. Initial Console Provisioning & Version Selection</b></summary>

The gateway deployment began with the selection of the **Current Stable Version (2.8.1)** of pfSense CE to ensure a secure foundation for the hybrid cloud gateway.

**Manual Provisioning Steps:**
* **Version Audit**: Selected the AMD64 ISO specifically optimized for virtualized environments.
* **Environment Detection**: Verified successful detection of the **VMware Virtual Machine** platform to ensure driver compatibility.

**Implementation Evidence:**
![pfSense Version Selection](../assets/pfsense-version-select.png)  
*Figure 1: Selection of the 2.8.1-RELEASE for the project foundation.*

![Environment Detection](../assets/pfsense-vmware-detect.png)  
*Figure 2: System confirmation of the VMware virtualized environment.*

</details>

<details>
<summary><b>2. Manual Interface Handshake (WAN/LAN Assignment)</b></summary>

A critical security step involved the manual assignment of physical interfaces to virtual network segments to prevent traffic "leakage" between the internal lab and the external host network.

**Configuration Audit:**
* **WAN Interface (le0)**: Manually mapped to the external-facing virtual adapter to receive a DHCP address via VMware NAT.
* **LAN Interface (le1)**: Mapped to the internal LAN segment to serve as the private gateway[cite: 2].

**Interface Mapping Proof:**
![WAN Assignment](../assets/pfsense-wan-assign.png)  
*Figure 3: Manual selection of the 'le0' interface for external WAN connectivity.*

![LAN Assignment](../assets/pfsense-lan-assign.png)  
*Figure 4: Manual selection of the 'le1' interface for the internal lab network.*

</details>

<details>
<summary><b>3. Gateway IP Logic & Enterprise DHCP</b></summary>

To maintain a centralized enterprise environment, **Windows Server 2022** manages DHCP, while pfSense acts as the dedicated gateway[cite: 2].

**The Routing Bridge:**
I manually assigned a static LAN IP of **192.168.10.254** to the pfSense gateway[cite: 2]. In the Windows DHCP Manager, I configured **Scope Option 003 (Router)** to point to this exact address, ensuring all clients automatically discover their exit path[cite: 2].

**Implementation Proof:**
![Static LAN Configuration](../assets/pfsense-static-lan.png)  
*Figure 5: Manual assignment of the 192.168.10.254 gateway IP address.*

![DHCP Scope Options](../assets/dhcp-scope-options.png)  
*Figure 6: Windows DHCP Manager confirming the active '003 Router' configuration.*

</details>

<details>
<summary><b>4. Final System Audit & Connectivity Validation</b></summary>

Once the handshake between the Server and Gateway was complete, a final audit was performed on the Windows 11 workstation.

**Verification Metrics:**
* **System Integrity**: Web dashboard confirms the system is on the latest version with active Netgate services[cite: 2].
* **Gateway Acquisition**: Client `ipconfig` results confirm the workstation is successfully pointed to the pfSense gateway[cite: 2].
* **Transit Proof**: Successful ping to `8.8.8.8` with 0% packet loss confirms the hybrid bridge is fully operational[cite: 2].

**Connectivity Victory:**
![pfSense Dashboard](../assets/pfsense-dashboard.png)  
*Figure 7: Final web dashboard showing healthy WAN/LAN interfaces and system version.*

![Connectivity Test](../assets/client-connectivity-test.png)  
*Figure 8: Successful end-to-end internet transit from the internal domain client.*

</details>

---

## 💡 Engineering Insights
This phase proved that a secure network is not "auto-installed"—it is manually architected[cite: 2]. By documenting the **Interface Assignments** and **Static IP definitions**, this project demonstrates the ability to manage low-level network architecture before moving to high-level cloud synchronization[cite: 2].

#Cybersecurity #NetworkEngineering #pfSense #ActiveDirectory #HomeLab #WorldSkills2028
