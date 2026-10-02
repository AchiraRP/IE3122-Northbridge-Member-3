# IE3122 – Northbridge Savings & Finance
## Member 3 – Network Hardening Configurations

This repository contains Member 3's individual practical work for the **IE3122 Network Security** group assignment, **Northbridge Savings & Finance Network Security Upgrade**.

### Student
- **Name:** Pathiraja P.M.A.R
- **Student ID:** IT24102763
- **Role:** Member 3

## Configurations

### 1. Port Security
**Threat Addressed:** Threat 3.2 – DHCP Spoofing at Branch Offices

Port Security was implemented on **SW-BR FastEthernet0/2** using:
- Access mode
- Maximum 1 secure MAC address
- Sticky MAC learning
- Shutdown violation mode

The configuration was tested using a legitimate PC and a Rogue-PC to demonstrate violation detection, err-disabled behavior, recovery, and final connectivity restoration.

### 2. Extended ACL – BYOD Network Isolation
**Threat Addressed:** Threat 4.2 – Malware via BYOD / Unmanaged Personal Devices

A separate **BYOD VLAN 50** was created and isolated from the internal Head Office network using an Extended ACL named **BYOD-ISOLATION**.

The ACL blocks traffic from:
`192.168.50.0/24`

to:
`192.168.10.0/24`

while permitting other traffic.

### Originally Assigned UplinkFast

UplinkFast was originally assigned as Member 3's second practical configuration. It was not implemented because the available Cisco 2960 Packet Tracer IOS did not provide the required `spanning-tree uplinkfast` command, and the assigned topology did not contain a redundant uplink path for a meaningful UplinkFast failover demonstration.

Extended ACL was therefore implemented as the second practical configuration.

## Repository Contents

- **01-Original** – Original Packet Tracer topology
- **02-Working** – Working Packet Tracer files
- **03-Screenshots** – Practical screenshots and evidence
- **04-Commands** – Command scripts
- **05-Final** – Final Packet Tracer files, screenshots, commands, and practical logs
- **Viva** – Viva preparation materials
- **Member3_Network_Hardening_Configurations_Structure.docx** – Member 3 network hardening document

## Final Packet Tracer Files

- `Northbridge_Member3_PortSecurity.pkt`
- `Northbridge_Member3_ExtendedACL.pkt`

## Evidence

The repository includes configuration screenshots, violation testing, recovery evidence, ACL verification, command scripts, and detailed practical logs.

---

**IE3122 Network Security – Northbridge Savings & Finance Network Security Upgrade**

## Threat Models Related to My Configurations

### Threat 3.2 – DHCP Spoofing at Branch Offices

**Configuration:** Port Security  
**Control:** Layer 2 Access Security Hardening

**Asset:** Branch office network and connected client devices.

**Vulnerability:** Weak physical security at branch offices can allow an unauthorised device to be connected to a switch access port.

**Threat:** An attacker or unauthorised person physically connects a rogue device to the branch network.

**Exploit:** The attacker uses the unauthorised device to participate in the local network and potentially support a rogue DHCP attack.

**Attack:** A rogue DHCP server/device can provide false network configuration information to legitimate clients.

**Impact:** Traffic interception, possible man-in-the-middle conditions, and network disruption.

**Risk:** Medium.

**How my configuration helps:** Port Security on **SW-BR FastEthernet0/2** restricts the port to one authorised MAC address. Sticky MAC learning records the legitimate device, while shutdown violation mode places the port into an err-disabled state when an unauthorised MAC is detected.

### Threat 4.2 – Malware via BYOD / Unmanaged Personal Devices

**Configuration:** Extended ACL – BYOD Network Isolation  
**Control:** Network Segmentation

**Asset:** Internal Head Office network and internal systems.

**Vulnerability:** Unmanaged BYOD devices may introduce security risks when connected to the organisation's network.

**Threat:** A compromised or malware-infected BYOD device is connected to the network.

**Exploit:** Malware on the device attempts to communicate with protected internal resources.

**Attack:** The compromised BYOD device attempts direct communication with the internal Head Office subnet.

**Impact:** Increased exposure of internal systems to malware and lateral movement.

**How my configuration helps:** **VLAN 50 (BYOD_GUEST)** was created for BYOD devices. The **BYOD-ISOLATION** ACL blocks traffic from **192.168.50.0/24** to **192.168.10.0/24**. The ACL provides network isolation; it does not detect or remove malware.

### Configuration-to-Threat Mapping

| Configuration | Threat | Main Security Purpose |
|---|---|---|
| Port Security | Threat 3.2 – DHCP Spoofing at Branch Offices | Restrict unauthorised device insertion |
| Extended ACL | Threat 4.2 – Malware via BYOD / Unmanaged Personal Devices | Isolate BYOD traffic from the internal network |
