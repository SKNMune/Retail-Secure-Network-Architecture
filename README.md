# Secure Retail Network Architecture: Departmental Isolation & Edge Security

## Project Overview
This project simulates a secure network infrastructure for a high-volume retail environment (e.g., Pharmacy/Grocery). The primary goal was to implement **VLAN Segmentation** and **Access Control Lists (ACLs)** to ensure data privacy and compliance (HIPAA/PCI-DSS) while maintaining operational efficiency.

## Key Technical Features
*   **Router-on-a-Stick (RoaS):** Implemented on a Cisco 2911 to facilitate Inter-VLAN routing across four distinct departments.
*   **VLAN Segmentation:** 
    *   **VLAN 10 (Management):** Isolated control plane for network infrastructure.
    *   **VLAN 20 (HR):** High-privacy zone for payroll and insurance data.
    *   **VLAN 30 (Team Leads):** Management tier with access to staff resources.
    *   **VLAN 40 (Staff/Associates):** Restricted "island" for point-of-sale and floor operations.
*   **Layer 3 Security (ACLs):** 
    *   Enforced "Least Privilege" access.
    *   Prevented unauthorized lateral movement between sensitive departments.
    *   Implemented **NAT Overload** (PAT) for secure Internet egress to a simulated web server (8.8.8.8).
*   **Infrastructure Hardening:**
    *   **SSH v2** only for remote management (Telnet disabled).
    *   **VTY Access-Classes** to restrict management access to the IT subnet only.
    *   **Port Security** on Access Switches to mitigate MAC-spoofing and unauthorized device attachment.

## Business Logic & Design
As a Pharmacy Technician with 3 years of experience, I designed this topology to mirror real-world compliance requirements. 
*   **Scenario:** HR must be able to initiate contact with Staff for disciplinary/benefit reasons, but Staff devices are strictly prohibited from "peeking" into HR’s payroll records. This was achieved using the `established` keyword in Extended ACLs.

## How to Test
1. Open `Store_Network.pkt` in Cisco Packet Tracer.
2. From a PC in **VLAN 20 (HR)**, attempt to ping the **Management IP (192.168.10.1)**. Traffic will be denied.
3. Open the Web Browser on any PC and navigate to `google.com`. Traffic will be translated via NAT and successfully reach the simulated ISP server.
