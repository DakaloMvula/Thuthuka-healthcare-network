# Thuthuka Health Group – Secure Multi-Site Healthcare Network

**Enterprise Network Design, Implementation and Security Using Cisco Packet Tracer**

## Project Overview

This project demonstrates the design, implementation, configuration and testing of a secure, scalable and resilient enterprise network for **Thuthuka Health Group**, a fictional private healthcare organisation operating across three locations in South Africa.

The network was developed using **Cisco Packet Tracer** to simulate a realistic healthcare IT environment supporting clinical operations, administrative services, medical devices, patient and staff wireless connectivity, centralised network services and secure inter-site communication.

The primary objective was to design a network infrastructure that balances **security, availability, performance, scalability and operational continuity**, while addressing the specific challenges associated with healthcare environments.

The implementation incorporates VLAN segmentation, inter-VLAN routing, dynamic routing, gateway redundancy, access control lists, network address translation, secure device management and access-layer security controls.

The project also includes configuration verification, connectivity testing, troubleshooting and technical documentation.

---

## 1. Project Objectives

The main objectives of the project were to:

- Design a secure network connecting three geographically separated healthcare facilities.
- Implement logical network segmentation using VLANs.
- Protect sensitive clinical systems and medical equipment from unauthorised network access.
- Provide separate wireless networks for patients and staff.
- Establish secure communication between the organisation's sites.
- Implement dynamic routing and redundant network paths.
- Improve network availability through gateway and link redundancy.
- Provide centralised network services, including DHCP and DNS.
- Configure Network Address Translation (NAT/PAT) for internet connectivity.
- Implement access-layer security mechanisms to mitigate common network attacks.
- Enable secure network administration, authentication, logging and time synchronisation.
- Validate the implementation through practical testing and troubleshooting.
- Develop a scalable architecture capable of supporting additional healthcare facilities.

## 2. Organisation and Network Requirements

Thuthuka Health Group consists of three sites with different operational requirements.

| Location | Facility | Approximate Staff | Main Functions |
|---|---|---:|---|
| Sandton | Flagship Hospital and Head Office | 320 | Clinical services, administration, radiology, ICU, centralised servers and management |
| Polokwane | Regional Hospital | 90 | Clinical services, administration, medical devices and wireless connectivity |
| Rustenburg | Day Clinic | 25 | Clinical operations, medical devices and wireless connectivity |

### Sandton – Flagship Hospital

Sandton functions as the organisation's primary network hub.

It hosts the centralised server infrastructure, clinical applications, administrative systems, PACS services, medical-device networks and wireless connectivity.

The site uses a hierarchical switching architecture with two multilayer core switches to support routing, redundancy and VLAN segmentation.

### Polokwane – Regional Hospital

Polokwane connects to the Sandton network through a WAN connection.

The local network includes a router, access switches, clinical workstations, administrative devices and wireless connectivity.

The design uses router-on-a-stick inter-VLAN routing and dynamic routing to communicate with the other sites.

### Rustenburg – Day Clinic

Rustenburg uses a smaller network architecture appropriate for a day clinic.

The site includes a router, access switch, clinical workstation and wireless access point.

The network provides local VLAN segmentation and inter-site communication while maintaining security policies for patient wireless traffic.

---

## 3. Technologies and Tools

| Technology | Purpose |
|---|---|
| Cisco Packet Tracer | Network simulation, implementation and testing |
| Cisco IOS CLI | Device configuration and troubleshooting |
| VLANs | Logical segmentation of network traffic |
| IEEE 802.1Q | VLAN trunking |
| VLSM | Efficient IP address allocation |
| Inter-VLAN Routing | Communication between authorised VLANs |
| OSPF | Dynamic routing between healthcare sites |
| HSRP | Redundant default gateways |
| EtherChannel | Link aggregation between core switches |
| Rapid PVST+ | Loop prevention and faster spanning-tree convergence |
| ACLs | Traffic filtering and network isolation |
| NAT/PAT | Translation of private addresses for internet access |
| DHCP | Automatic IP address allocation |
| DNS | Domain name resolution |
| SSHv2 | Secure remote network administration |
| AAA/RADIUS | Centralised authentication configuration |
| DHCP Snooping | Protection against rogue DHCP servers |
| Dynamic ARP Inspection | Protection against ARP spoofing |
| Port Security | Restriction of access through switch ports |
| NTP | Network time synchronisation |
| Syslog | Centralised event logging configuration |

---

## 4. Network Architecture

The network follows a distributed, multi-site architecture, with Sandton acting as the primary service and management location.

### High-Level Topology

```text
                         INTERNET / ISP
                               |
                               |
                       R1 - SANDTON EDGE
                        /      |      \
                       /       |       \
                     R2       MLS1      R3
                 POLOKWANE     ||    RUSTENBURG
                     |         ||        |
                    PSW1      MLS2      RSW1
                     |         |         |
                    PSW2    Access     Clinical PC
                     |      Switches   Wireless AP
                Clinical/      |
                Admin PCs   Clinical PCs
                Wireless    Admin PCs
                            PACS
                            ICU Devices
                            Servers
                            Wireless APs
```

*Simplified logical representation. The Packet Tracer file contains the detailed device connections and WAN topology.*

### Architecture Components

**Core Layer – Sandton**

Two Cisco multilayer switches, MLS1 and MLS2, provide Layer 3 routing, VLAN interfaces and redundant gateway functionality.

**Access Layer**

Access switches connect workstations, medical equipment, servers and wireless access points to their assigned VLANs.

**WAN Layer**

Three routers provide communication between Sandton, Polokwane and Rustenburg.

**Internet Edge**

R1 serves as the primary internet-facing router and provides NAT/PAT functionality.

**Server Infrastructure**

Centralised services are hosted at Sandton, including DNS, monitoring and other simulated healthcare network services.

---

## 5. IP Addressing and Subnet Design

The network uses private IPv4 addressing from the `10.0.0.0/8` address space.

VLSM was used to allocate subnets according to the size and operational requirements of each site.

### Site Address Allocation

| Site | Address Allocation |
|---|---|
| Sandton | 10.10.0.0/20 |
| Polokwane | 10.10.16.0/22 |
| Rustenburg | 10.10.20.0/23 |
| Internal WAN links | 10.255.0.0 address space |
| Simulated public network | 203.0.113.0/30 |

### Sandton VLAN Addressing

| VLAN | Name | Subnet | Default Gateway |
|---|---|---|---|
| 10 | MANAGEMENT | 10.10.2.64/26 | 10.10.2.65 |
| 20 | ADMIN | 10.10.1.0/25 | 10.10.1.1 |
| 30 | CLINICAL | 10.10.0.0/24 | 10.10.0.1 |
| 40 | MEDICAL-DEVICES | Reserved for medical-device segmentation | As configured |
| 50 | PACS | 10.10.1.128/26 | 10.10.1.129 |
| 60 | ICU-DEVICES | 10.10.1.192/26 | 10.10.1.193 |
| 70 | GUEST-WIFI | 10.10.4.0/23 | 10.10.4.1 |
| 80 | STAFF-WIFI | 10.10.6.0/24 | 10.10.6.1 |
| 90 | SERVERS | 10.10.2.0/26 | 10.10.2.1 |
| 100 | VOICE | 10.10.3.0/24 | 10.10.3.1 |
| 999 | NATIVE | No IP address | N/A |

The VLAN table reflects the addressing used or planned during implementation. The final Packet Tracer configuration is the authoritative reference for individual interfaces.

### Polokwane Addressing

| VLAN | Purpose | Subnet | Gateway |
|---|---|---|---|
| 10 | Management | 10.10.17.64/27 | 10.10.17.65 |
| 20 | Administration | 10.10.16.128/26 | 10.10.16.129 |
| 30 | Clinical | 10.10.16.0/25 | 10.10.16.1 |
| 40 | Medical Devices | 10.10.16.192/27 | 10.10.16.193 |
| 70 | Patient Wi-Fi | 10.10.17.0/26 | 10.10.17.1 |
| 80 | Staff Wi-Fi | 10.10.16.224/27 | 10.10.16.225 |

### Rustenburg Addressing

| VLAN | Purpose | Subnet | Gateway |
|---|---|---|---|
| 10 | Management | 10.10.20.64/27 | 10.10.20.65 |
| 30 | Clinical | 10.10.20.0/26 | 10.10.20.1 |
| 40 | Medical Devices | 10.10.20.160/28 | 10.10.20.161 |
| 70 | Patient Wi-Fi | 10.10.20.96/27 | 10.10.20.97 |
| 80 | Staff Wi-Fi | 10.10.20.128/27 | 10.10.20.129 |

This addressing structure provides logical separation between departments and allows individual site networks to be managed independently.

---

## 6. VLAN Segmentation

VLANs were implemented to separate network traffic according to operational function and security requirements.

The main VLAN categories include:

- Management infrastructure
- Administrative workstations
- Clinical workstations
- Medical and ICU devices
- PACS systems
- Patient wireless access
- Staff wireless access
- Centralised servers
- Voice services

This approach reduces unnecessary broadcast traffic and creates logical security boundaries between different systems.

For example, clinical workstations and medical devices are placed into separate VLANs so that communication between them can be controlled using access control policies.

Patient wireless traffic is also separated from internal healthcare systems.

### VLAN Trunking

IEEE 802.1Q trunking was configured to transport multiple VLANs between switches.

The implementation includes:

- Explicit trunk mode configuration.
- Native VLAN 999.
- Restricted allowed VLAN lists.
- Disabled DTP negotiation on configured trunk interfaces.
- Verification of active and forwarding VLANs.

Example verification command:

```cisco
show interfaces trunk
```

The Sandton core switch MLS1 was verified with operational trunks on Port-channel1, FastEthernet0/1 and FastEthernet0/2.

Polokwane switches PSW1 and PSW2 and Rustenburg switch RSW1 were also configured and verified.

---

## 7. Inter-VLAN Routing

Inter-VLAN routing allows devices in different VLANs to communicate when permitted by the network's security policies.

### Sandton

Inter-VLAN routing is performed by MLS1 and MLS2 using switched virtual interfaces (SVIs).

Each SVI represents a VLAN gateway and provides Layer 3 connectivity.

### Polokwane and Rustenburg

Router-on-a-stick was implemented using IEEE 802.1Q router subinterfaces.

Each router subinterface corresponds to a specific VLAN.

This approach provides an efficient routing solution for smaller sites without requiring additional multilayer switches.

---

## 8. Dynamic Routing Using OSPF

Open Shortest Path First (OSPF) was implemented to support communication between the three healthcare facilities.

OSPF enables routers to exchange routing information dynamically and select appropriate paths between networks.

### Implementation

- OSPF process 1 was used.
- WAN connections participate in Area 0.
- Internal site networks are advertised through routing.
- Routers R1, R2 and R3 establish routing adjacencies.
- Alternative WAN connectivity is incorporated into the topology.

### Benefits

- Automatic exchange of routing information.
- Reduced dependence on manually maintained routes.
- Support for multiple interconnected sites.
- Faster adaptation to routing topology changes.
- Improved scalability for additional healthcare locations.

### Verification

```cisco
show ip ospf neighbor
show ip route
show ip protocols
```

OSPF neighbour relationships and learned inter-site routes were successfully observed during testing.

---

## 9. Network Redundancy and High Availability

Healthcare networks require high availability because network interruptions can affect access to clinical information and essential services.

Several redundancy mechanisms were incorporated into the design.

### 9.1 HSRP Gateway Redundancy

Hot Standby Router Protocol (HSRP) was configured on the Sandton multilayer switches.

HSRP provides a virtual default gateway that can remain available if the active gateway device fails.

The implementation distributes active gateway responsibilities between MLS1 and MLS2.

This reduces dependence on a single core switch.

### 9.2 EtherChannel

EtherChannel was configured between the core switches to aggregate multiple physical interfaces into one logical connection.

Benefits include:

- Increased aggregate bandwidth.
- Redundant physical connectivity.
- Simplified logical link management.

LACP was used for EtherChannel negotiation.

### 9.3 Rapid PVST+

Rapid Per-VLAN Spanning Tree Plus was configured on the Sandton core switches.

It provides loop prevention and supports faster convergence following network topology changes.

The design assigns different spanning-tree priorities to the core switches to distribute root-bridge responsibilities.

### 9.4 WAN Redundancy

The three-site WAN topology includes alternative routing paths.

OSPF supports route recalculation when network connectivity changes.

During previous testing, WAN connectivity was evaluated using continuous ping tests and routing verification.

---

## 10. Access Control Lists and Network Isolation

ACLs were implemented to control traffic between network segments and reduce unauthorised access.

### 10.1 Medical-Device Isolation

A named extended ACL, `MEDICAL-DEVICE-ISOLATION`, was configured to restrict traffic originating from the ICU medical-device network.

The intended security policy permits communication with an authorised monitoring server while denying other destinations.

Example protected network:

- ICU Devices: `10.10.1.192/26`
- Monitoring Server: `10.10.2.11`

The ACL is designed to limit unnecessary communication from medical equipment and reduce exposure to other internal systems.

During troubleshooting, ACL interface placement and direction were investigated to ensure traffic filtering occurred at the correct point.

### 10.2 Patient Wi-Fi Isolation

A separate extended ACL, `PATIENT-WIFI-ISOLATION`, was configured for patient wireless traffic.

The policy is designed to:

- Permit DNS requests to the authorised DNS server.
- Deny unauthorised access to private internal networks.
- Permit traffic to approved external destinations.

The ACL was applied inbound on the relevant patient VLAN routing interface.

### 10.3 Rustenburg Connectivity Exception

During testing, communication between a Rustenburg clinical PC and a patient wireless laptop was initially blocked by the patient isolation policy.

A specific host-to-host ACL exception was subsequently introduced for the test scenario.

This restored the required communication without removing the broader ACL.

**Security consideration:** The exception reduces isolation between patient and clinical networks. In a production healthcare environment, such access should require a documented business justification and security review.

---

## 11. Access-Layer Security

Several Layer 2 security controls were implemented or evaluated to protect access switches against common local network attacks.

### 11.1 DHCP Snooping

DHCP snooping was configured to help prevent unauthorised DHCP servers from distributing incorrect network configurations.

On ASW1, verification confirmed that DHCP snooping was enabled on VLANs 30 and 60.

Trusted and untrusted interfaces were defined to distinguish authorised DHCP infrastructure from client-facing connections.

### 11.2 Dynamic ARP Inspection

Dynamic ARP Inspection was configured to reduce the risk of ARP spoofing.

Verification on ASW1 confirmed that DAI was enabled and operational on VLANs 30 and 60.

### 11.3 Port Security

Port security formed part of the access-layer security design.

It is intended to restrict unauthorised devices from connecting to selected access ports.

Full operational verification of port-security enforcement was not captured in the final test evidence.

### 11.4 Spanning-Tree Protection

PortFast and BPDU Guard were considered and configured on appropriate access interfaces.

These features support faster client connectivity and help protect the switching topology against unexpected bridge protocol data units.

---

## 12. DHCP and DNS Services

Centralised network services were incorporated to simplify network administration and improve consistency.

### 12.1 DHCP

DHCP was configured to assign IP addressing information automatically to supported client networks.

DHCP configuration includes:

- IP address pools.
- Subnet masks.
- Default gateways.
- DNS server addresses.
- Excluded IP address ranges.

DHCP reduces manual configuration requirements and supports easier network administration.

### 12.2 DNS

A DNS server was configured at:

`10.10.2.10`

The DNS service provides name resolution for the simulated network.

### DHCP and DNS Testing

A Sandton Clinical PC successfully received the following network configuration:

| Parameter | Observed Value |
|---|---|
| IPv4 Address | 10.10.0.18 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 10.10.0.1 |
| DHCP Server | 10.10.0.2 |
| DNS Server | 10.10.2.10 |

DNS testing successfully resolved the simulated `www.google.com` record to `198.51.100.10`.

The DNS server also responded to four ICMP echo requests with 0% packet loss.

An initial DNS timeout was observed before successful resolution.

---

## 13. Internet Connectivity and NAT/PAT

Network Address Translation with Port Address Translation was configured on the Sandton edge router, R1.

PAT enables multiple private internal IP addresses to share a public-facing address when communicating with external networks.

### NAT Configuration

The implementation uses:

- Inside interfaces connected to internal and WAN networks.
- Outside interface GigabitEthernet0/2.
- Standard ACL 10 to identify eligible internal addresses.
- PAT overload on the outside interface.
- A default route toward the simulated ISP.

Example configuration:

```cisco
access-list 10 permit 10.10.0.0 0.0.255.255

ip nat inside source list 10 interface GigabitEthernet0/2 overload
```

Public-facing interface:

`203.0.113.2`

ISP next hop:

`203.0.113.1`

### Verification

```cisco
show ip nat translations
show ip nat statistics
show ip route
```

The NAT/PAT configuration and default route were verified.

However, the final captured translation table did not contain an active translation. Therefore, the available evidence confirms configuration rather than complete end-to-end NAT functionality.

The public addresses used in this project belong to documentation address ranges and are used for simulation.

---

## 14. Secure Network Management

Secure network administration was implemented to reduce reliance on insecure management protocols.

### 14.1 SSH Version 2

SSHv2 was enabled on MLS1 for encrypted remote management.

Verification confirmed:

```text
SSH Enabled - version 2.0
```

### 14.2 AAA and RADIUS

Authentication, Authorisation and Accounting (AAA) was configured with RADIUS authentication and local fallback.

The configured RADIUS server address is:

`10.10.2.10`

This provides a foundation for centralised network administrator authentication.

### 14.3 Network Time Protocol

NTP was configured to synchronise network device clocks.

MLS1 successfully synchronised with:

`10.255.0.14`

Accurate timestamps are important for troubleshooting, monitoring and security investigations.

### 14.4 Centralised Logging

Remote syslog was configured to forward network events to:

`10.10.2.10`

Centralised logging supports incident investigation, troubleshooting and operational monitoring.

The available verification confirms logging configuration, although successful end-to-end log delivery was not separately demonstrated.

### 14.5 Additional Device Hardening

The configuration includes several baseline security measures:

- Device hostnames.
- Encrypted stored password representations.
- Privileged EXEC authentication.
- Console and remote-access authentication.
- Login banners.
- Session timeout configuration.
- SSH-based management.
- Restricted management access where configured.

These controls help establish a more manageable and secure network environment.

---

## 15. Testing and Verification

The project was tested using Cisco IOS verification commands and simulated network traffic.

The testing process included configuration inspection, connectivity tests, routing checks, security policy validation and troubleshooting.

### Test Summary

| Test Area | Verification | Outcome |
|---|---|---|
| VLAN segmentation | VLAN database and interface checks | Verified on tested switches |
| 802.1Q trunking | `show interfaces trunk` | Passed on tested links |
| Native VLAN configuration | Trunk inspection | VLAN 999 confirmed |
| OSPF routing | Neighbour and routing table checks | Operational |
| HSRP | Gateway configuration inspection | Configured; full failover evidence limited |
| WAN redundancy | Connectivity and routing tests | Tested during implementation |
| Patient Wi-Fi isolation | ACL inspection and connectivity tests | Filtering demonstrated; test exception added |
| Medical-device isolation | ACL configuration and placement checks | Configured; full policy validation incomplete |
| DHCP | Client IP configuration | Passed for tested client |
| DNS | `nslookup` and ping | Passed after initial timeout |
| NAT/PAT | NAT configuration and translation inspection | Partially verified |
| DHCP snooping | Switch security inspection | Enabled on tested VLANs |
| Dynamic ARP Inspection | Switch security inspection | Enabled on tested VLANs |
| SSH | `show ip ssh` | Passed |
| AAA/RADIUS | Running configuration inspection | Configured |
| NTP | `show ntp associations` | Synchronised |
| Syslog | Running configuration inspection | Configured; delivery not independently verified |

### Useful Verification Commands

**Switching**

```cisco
show vlan brief
show interfaces trunk
show spanning-tree
show etherchannel summary
```

**Routing**

```cisco
show ip interface brief
show ip route
show ip ospf neighbor
show standby brief
```

**Security**

```cisco
show access-lists
show port-security
show ip dhcp snooping
show ip arp inspection
```

**Network Services**

```cisco
show ip dhcp binding
show ip nat translations
show ip nat statistics
show ip ssh
show ntp associations
```

**Client Connectivity**

```text
ipconfig /all
ping <destination-ip>
tracert <destination-ip>
nslookup <domain-name>
```

---

## 16. Troubleshooting and Lessons Learned

A significant part of this project involved identifying and resolving network configuration problems.

### 16.1 Trunk Interfaces Not Forwarding VLANs

**Problem:** During initial verification, the Polokwane switch trunks showed no VLANs in the spanning-tree forwarding state.

**Investigation:** The trunk interfaces and spanning-tree status were inspected using Cisco IOS commands.

**Outcome:** Subsequent checks confirmed that the permitted VLANs had entered the forwarding state.

**Lesson learned:** An operational trunk does not necessarily mean that all VLANs are immediately forwarding traffic. Spanning-tree convergence must also be considered.

### 16.2 Patient Wireless Connectivity Blocked

**Problem:** A Rustenburg patient wireless laptop could not communicate with a clinical workstation.

**Cause:** The inbound patient Wi-Fi isolation ACL denied traffic to internal private networks.

**Resolution:** A specific host-to-host permit statement was introduced before the broader deny rule.

**Outcome:** Communication succeeded after the ACL adjustment.

**Lesson learned:** ACL order and rule specificity directly affect traffic flow. Security exceptions should be narrowly scoped and carefully documented.

### 16.3 Medical-Device ACL Placement

**Problem:** During security testing, the medical-device isolation policy required investigation because ACL placement was inconsistent between relevant routing interfaces.

**Investigation:** Interface-level ACL assignments and access-list rules were reviewed.

**Lesson learned:** Extended ACL placement and direction are essential to effective traffic filtering. Inbound filtering can prevent unauthorised traffic from being routed further into the network.

### 16.4 NAT/PAT Verification

**Problem:** The NAT translation table remained empty during verification despite NAT/PAT configuration being present.

**Investigation:** NAT interface assignments, the overload rule, the NAT ACL and the default route were inspected.

**Outcome:** The configuration was verified, but an active translation was not captured in the final evidence.

**Lesson learned:** Configuration verification and functional testing are different activities. A correctly configured feature should not be reported as fully operational without sufficient evidence.

### 16.5 Spanning-Tree and BPDU Guard

**Problem:** BPDU Guard affected a switch port used for infrastructure connectivity during earlier configuration work.

**Cause:** Spanning-tree security settings were applied to an interface where BPDUs could legitimately be received.

**Lesson learned:** BPDU Guard and PortFast should be applied according to the role of each interface, rather than indiscriminately across all ports.

### 16.6 DNS Resolution Delay

**Problem:** A DNS lookup initially timed out before successfully resolving the requested hostname.

**Outcome:** The configured DNS server subsequently returned the expected record.

**Lesson learned:** Testing should record intermittent failures and delays rather than only the final successful result.

---

## 17. Security Considerations

The network was designed around several cybersecurity principles.

### Network Segmentation

Clinical, administrative, medical-device and wireless traffic are separated into logical networks.

### Least-Privilege Access

ACLs restrict communication according to operational requirements.

### Defence in Depth

Multiple security mechanisms are incorporated, including VLANs, ACLs, DHCP snooping, DAI, SSH and AAA.

### Availability

Gateway redundancy, link aggregation, dynamic routing and alternative WAN paths help reduce single points of failure.

### Monitoring and Accountability

Centralised logging, time synchronisation and authentication configuration support network administration and incident investigation.

### Healthcare Data Protection

The design considers the importance of protecting healthcare systems and sensitive operational information.

Although this is a simulated environment without real patient records, the architecture reflects security principles relevant to healthcare organisations and data-protection obligations such as South Africa's Protection of Personal Information Act (POPIA).

This simulation does not constitute a formal compliance assessment.

---

## 18. Challenges and Limitations

The project was implemented in a simulated environment and has several limitations.

1. Packet Tracer does not reproduce every capability of production Cisco IOS hardware.
2. Some enterprise security features have limited simulation support.
3. Real healthcare applications and medical equipment were represented using simulated devices and services.
4. Not every configured security control was subjected to a complete functional attack or failover test.
5. NAT/PAT configuration was verified, but an active translation was not captured in the final evidence.
6. Some security exceptions were introduced for testing and would require review before production deployment.
7. Production-grade monitoring, firewalling and application-level security would require additional technologies.

These limitations should be considered when interpreting the test results.

---

## 19. Future Improvements

The following enhancements could further improve the network.

### Next-Generation Firewall

Deploy a dedicated firewall at the internet edge to provide application-aware filtering, intrusion prevention and enhanced traffic inspection.

### Stronger Medical-Device Segmentation

Introduce more granular access policies and dedicated security zones for medical and IoT equipment.

### Centralised Monitoring

Integrate a network monitoring platform to collect performance metrics, device status, logs and security alerts.

### Automated Configuration Management

Use automation tools such as Ansible or Python to standardise network configurations and simplify administration.

### Improved Authentication

Introduce stronger administrator authentication controls and more comprehensive AAA policy enforcement.

### Disaster Recovery

Develop backup and recovery procedures for network configurations, critical services and healthcare systems.

### Additional Clinics

Extend the addressing and WAN design to accommodate two additional day clinics without major restructuring.

### Further Validation

Perform comprehensive HSRP failover, WAN failover, NAT/PAT, port-security and security-policy testing with documented before-and-after results.

---

## 20. Repository Structure

A recommended repository layout is:

```text
thuthuka-healthcare-network/
│
├── README.md
│
├── packet-tracer/
│   └── Thuthuka-Health-Group.pkt
│
├── screenshots/
│   ├── network-topology.png
│   ├── vlan-trunk-verification.png
│   ├── ospf-routing.png
│   ├── access-layer-security.png
│   ├── dhcp-dns-verification.png
│   ├── nat-pat-configuration.png
│   └── network-management.png
│
└── documentation/
    └── test-plan.pdf
```

*The structure above is recommended. Only include files that have actually been created.*

---

## 21. How to Open the Project

1. Install a compatible version of Cisco Packet Tracer.
2. Clone or download this GitHub repository.
3. Navigate to the `packet-tracer` directory.
4. Open the `.pkt` project file in Cisco Packet Tracer.
5. Allow the simulated network to initialise and routing protocols to converge.
6. Inspect the topology and device configurations.
7. Use the verification commands documented above to test network functionality.

Some devices may require authentication to access privileged configuration modes.

**Security note:** The publicly shared version should use demonstration-only credentials. Do not publish reusable passwords, shared secrets or real organisational information.

---

## 22. Skills Demonstrated

This project demonstrates practical knowledge and experience in:

- Enterprise network architecture
- Cisco router and switch configuration
- IPv4 addressing and VLSM
- VLAN design and implementation
- IEEE 802.1Q trunking
- Inter-VLAN routing
- OSPF dynamic routing
- HSRP gateway redundancy
- EtherChannel and LACP
- Rapid PVST+ and spanning-tree protection
- Access control lists
- Wireless network segmentation
- DHCP and DNS configuration
- NAT/PAT
- Network access security
- Secure device management
- AAA and RADIUS configuration
- Network monitoring fundamentals
- Connectivity testing
- Network troubleshooting
- Technical documentation

---

## 23. Conclusion

The Thuthuka Health Group project demonstrates the practical implementation of a secure multi-site healthcare network using Cisco Packet Tracer.

The network integrates three geographically separated facilities through dynamic routing and a structured IP addressing scheme, while using VLAN segmentation and access control policies to separate clinical, administrative, medical-device and wireless traffic.

At the Sandton headquarters, multilayer switching, HSRP, EtherChannel and spanning-tree technologies provide a foundation for network availability and resilience. Additional controls such as DHCP snooping, Dynamic ARP Inspection, SSH, AAA and centralised logging strengthen the network's security and manageability.

Practical testing confirmed several important functions, including VLAN trunking, OSPF connectivity, DHCP address assignment, DNS resolution, SSH operation and NTP synchronisation. Other controls were verified at configuration level, with remaining limitations documented.

The project strengthened practical skills in network design, implementation, security configuration, troubleshooting and technical reporting, while demonstrating how enterprise networking principles can be applied to a realistic healthcare scenario.

---

## Author

**Network Design and Implementation Project**

BSc Information Technology – Security and Network Engineering

**Tools:** Cisco Packet Tracer and Cisco IOS

**Project Type:** Academic / Portfolio Project

**Environment:** Simulated Healthcare Enterprise Network

**Disclaimer:** Thuthuka Health Group is a fictional organisation used for educational purposes. All network configurations, IP addresses and services are part of a simulated environment and do not represent a live healthcare infrastructure.
