# Phase 1: Networking Foundations & Enterprise Integration

This phase marks the successful establishment of the core infrastructure. The primary goal was to bridge an internal Active Directory environment with a secure pfSense gateway to allow controlled external traffic transit.

## 🏗️ Virtual Network Architecture
The environment is hosted on **VMware Workstation Pro** using custom **LAN Segments** to isolate laboratory traffic from the host machine.

*   **Gateway (pfSense)**: Managed via a dual-homed configuration (WAN/LAN).
*   **Directory Services (Windows Server 2022)**: Hosting the `singh.com` forest and enterprise DHCP/DNS.
*   **Endpoint (Windows 11)**: A domain-joined workstation utilizing dynamic addressing.

---

## 🛠️ Technical Deep-Dive (Configuration receipts)
*Click the toggles below to explore the specific configurations implemented in this phase.*

<details>
<summary><b>1. Gateway Deployment & WAN/LAN Handshake</b></summary>

### Interface Strategy
The gateway was deployed using the **AMD64 ISO** specifically optimized for virtual machines. This ensures high-performance packet processing within the VMware environment.

*   **WAN Interface**: Receives an external IP via VMware's NAT service to facilitate internet reachability.
*   **LAN Interface**: Assigned a static internal address of `192.168.10.254`.

**Implementation Evidence:**
![pfSense Installation Image](../assets/pfsense-iso-selection.png)
*Figure 1: Selection of the AMD64 ISO optimized for virtual environments.*

![pfSense Dashboard Status](../assets/pfsense-dashboard-verified.png)
*Figure 2: The master dashboard showing the 'Up' status for both WAN and LAN interfaces.*

</details>

<details>
<summary><b>2. Enterprise DHCP & Scope Option 003</b></summary>

### The Routing Bridge
To maintain a centralized enterprise environment, DHCP is managed by **Windows Server 2022** rather than the firewall. 

**The Challenge:** Initially, internal clients could receive IP addresses but were unable to reach the internet because they lacked a "Default Gateway" instruction.

**The Resolution:** I configured **DHCP Scope Option 003 (Router)**. This critical instruction tells every device in the `singh.com` domain to use `192.168.10.254` (pfSense) as their exit door.

**Configuration Proof:**
![DHCP Scope Options](../assets/dhcp-scope-options.png)
*Figure 3: Windows DHCP Manager confirming the active '003 Router' configuration.*

</details>

<details>
<summary><b>3. Client-Side Authentication & Connectivity Validation</b></summary>

### Final System Audit
A "Clean State" audit was performed on the Windows 11 workstation. By switching the adapter to **Automatic (DHCP)**, the client successfully inherited its identity and routing instructions from the server.

**Verification Metrics:**
*   **Domain Identification**: Client correctly identifies the `singh.com` network.
*   **Gateway Acquisition**: `ipconfig` confirms `192.168.10.254` as the Default Gateway.
*   **Stress Test**: Successful ICMP echo request (ping) to `8.8.8.8` with 0% packet loss.

**Connectivity Proof:**
![Windows Client Success](../assets/client-connectivity-test.png)
*Figure 4: The 'Victory Screen'—confirmed IP lease and successful internet transit.*

</details>

---

## 💡 Engineering Insights
This phase proved that a Hybrid Gateway is more than just a firewall; it is a collaborative effort between **Directory Services** and **Network Routing**. By offloading DHCP to the Windows Server but keeping the Gateway on pfSense, we have created a professional environment that is ready for Phase 2: Security & Traffic Filtering.
