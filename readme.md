# Electric Petrol Site Network Design

**Author:** Ayobami Pase  
**Project Type:** Industry-Style Network Infrastructure Design  
**Scope:** Layer 1 to Layer 3 Design, Prototype Implementation, WAN Routing, and Perimeter Security

---

## Overview

This project documents the complete network design and implementation for a greenfield **Electric Petrol Site** development. The site layout (minimum 400m × 200m) and building functions were agreed during initial client consultation, with preliminary floor plans provided for the forecourt building only.

The work spans six tasks, progressing from physical infrastructure through to WAN routing and perimeter security:

- **A1–A2** cover the Layer 1 physical design — containment routes, rack and cabinet placement, cable routing, access point and CCTV locations, and the full wirelist.
- **A3** delivers the Layer 2 logical design — VLAN architecture, switch configuration sheets, and logical topology diagrams.
- **A4** builds and tests a working switch prototype in GNS3, validating the Layer 2 design in a simulated environment.
- **A5** extends the network across a four-site WAN using OSPF multi-area routing, with the student site allocated as **Maynooth (Area 39, 10.39.0.0/16)**.
- **A6** adds perimeter security through FortiGate firewalls at each site, implementing WAN/LAN/DMZ segmentation, a full-mesh IPsec VPN, and remote access policies for mobile staff and contractors.

> This project is structured and documented as an **industry deployment**, not an academic exercise.

---

## Client Background

**Client:** [electric-petrol.ie]

Electric Petrol is a startup operating in the emerging EV infrastructure space, responding to European legislation phasing out combustion engine vehicles by 2035. The business model centres on deploying service stations across the island of Ireland equipped with local electrical storage and generation capacity.

Sites leverage nearby wind and solar farms to charge graphene-based super-capacitors, minimising reliance on the national grid. Stored energy can also be sold back to the grid at peak times, creating an additional revenue stream.

The client had registered their domain but had no existing IT or network infrastructure. This project covers the full network design for one site, from physical containment and cable routing through to VLAN architecture, prototype switch configuration, multi-site WAN routing, and perimeter firewall security.

---

## Repository Structure

```
networking/
│
├── A1/
│   ├── Site Containment Markup.drawio.pdf
│   ├── Forecourt Containment Markup.drawio.pdf
│   └── BOM.xlsx
│
├── A2/
│   └── wirelist.xlsx
│
├── A3/
│   ├── VLAN.xlsx
│   ├── SwitchConfig.xlsx
│   └── LogicalDiagram.pptx
│
├── A4/
│   ├── A4_GNS3_project
│   ├── A4_Test_Screenshots
│   ├── Switch_Configs
│   ├── Network_Plan
│   └── Topology
│
├── A5/
│   ├── A5_GNS3/
│   ├── scripts/
│   ├── testing/
│   ├── A5_WAN_Overview.drawio.png
│   ├── Topology.png
│   └── README.md
│
├── A6/
│   ├── diffs/
│   ├── fortigate_screenshots/
│   ├── A6_Topology.png
│   ├── A6_Topology_2.png
│   ├── A6_Topology_3.png
│   ├── A6_diagram.drawio.png
│   └── README.md
│
└── README.md
```

---

## A1 – Layer 1 Physical Design

### Scope

This phase covers rack and cabinet locations, distributor containment, cable routing, access point and CCTV placement, and the initial Bill of Materials.

### Deliverables

#### Marked-Up Site Drawing
- Site boundary (minimum 400m × 200m)
- Main building locations
- Underground containment routes
- External ducting
- Inter-building fibre runs
- Cabinet locations

#### Marked-Up Forecourt Building Drawing
- Cable tray routing
- Cabinet and rack locations
- Cabling termination points
- Wireless Access Points
- CCTV locations
- Equipment notes

#### Costed Bill of Materials (BOM)
Covers racks, UPS systems, PDUs, and installation labour.

---

## A2 – Wirelist Documentation

A wirelist provides port-to-port connectivity mapping, cabinet-to-device termination records, structured documentation for installers, and a future troubleshooting and audit reference.

**Deliverable:** `wirelist.xlsx`

This document corresponds directly to the site drawing (A1), forecourt drawing (A1), rack and cabinet layout, and patch panel assignments.

---

## A3 – Layer 2 Logical Design

### Deliverables

#### `VLAN.xlsx`
- VLAN IDs and names
- Purpose and IP addressing plan
- Subnet and gateway allocations

#### `SwitchConfig.xlsx`
- Hostname and management IP
- VLAN assignments (trunk and access ports)
- STP configuration
- Port descriptions

#### `LogicalDiagram.pptx`
- Core-to-distribution topology
- VLAN segmentation
- Inter-switch trunk links
- Device group and security zoning

The logical design corresponds directly to the physical design (A1) and wirelists (A2).

---

## A4 – Prototype Network Build

### Objective

Build a working prototype of the Electric Petrol site network using a minimum of 4 switches (one per Floor Distributor), with no internet connectivity, using provided device images only. Tested using **Azure Labs**.

### Requirements

- One switch per FD
- VLAN implementation
- Trunk configuration
- Inter-switch connectivity
- No external internet routing

### Deliverables

1. Final exported project file
2. Switch configuration listings

Configuration components include VLAN creation, access port assignment, trunk configuration, management IP configuration, and basic security hardening.

---

## A5 – WAN Prototype with OSPF

### Objective

Build a WAN prototype connecting four sites using OSPF multi-area routing. Each site has its own OSPF area, connected through a shared backbone (Area 0). The student site allocation is **Maynooth — Network `10.39.0.0/16`**.

### Site Allocation

| Site | Router(s) | Network | OSPF Area |
|------|-----------|---------|-----------|
| Head Office | IR-HO-100 | 10.0.0.0/16 | Area 0 |
| Data Centre 1 | ABR-DC1-101 | 10.1.0.0/16 | Area 1 |
| Data Centre 2 | ABR-DC2-102, IR-DC2-201 | 10.2.0.0/16 | Area 2 |
| **Maynooth** | **ABR-MY-139, IR-MY-239** | **10.39.0.0/16** | **Area 39** |

The WAN backbone runs on `10.255.255.0/24` connecting all four sites through Area 0. Loopback interfaces using the `10.255.254.0/24` range were configured on every router to provide a stable OSPF Router ID.

### Device List

| Device | Role | WAN IP (Gi0/3) | Local IP (Gi0/0) | Loopback |
|--------|------|----------------|------------------|----------|
| IR-HO-100 | Head Office router | 10.255.255.100/24 | 10.0.15.100/24 | 10.255.254.100/32 |
| ABR-DC1-101 | DC1 Area Border Router | 10.255.255.101/24 | 10.1.15.101/24 | 10.255.254.101/32 |
| ABR-DC2-102 | DC2 Area Border Router | 10.255.255.102/24 | 10.2.15.101/24 | 10.255.254.102/32 |
| IR-DC2-201 | DC2 Internal Router | — | 10.2.15.201/24 | 10.255.254.201/32 |
| **ABR-MY-139** | **My site ABR** | **10.255.255.139/24** | **10.39.15.101/24** | **10.255.254.139/32** |
| **IR-MY-239** | **My site IR** | — | **10.39.15.239/24** | **10.255.254.239/32** |

### Tests Conducted

1. **OSPF Neighbours (ABR-MY-139)** — Confirmed IR-MY-239 and IR-HO-100 listed as OSPF neighbours in FULL state.
2. **Routing Table (ABR-MY-139)** — Confirmed OSPF routes (O and O IA) present for all remote networks.
3. **Ping from PC1 to ABR-MY-139** — All 5 pings succeeded.
4. **Ping Across the WAN (IR-MY-239)** — Pinged IR-HO-100 (10.255.255.100) with 100% success rate, confirming OSPF routing works across the full WAN backbone.

### Deliverables

- GNS3 project files (`A5_GNS3/`)
- Router configuration scripts per device (`scripts/`)
- Test screenshots (`testing/`)
- WAN overview and topology diagrams

---

## A6 – Perimeter Firewall Design with FortiGate

### Objective

Deploy and configure four FortiGate 6.4 firewalls in GNS3, one per site, each with a WAN, LAN, and DMZ interface. All four sites are linked by a full-mesh IPsec VPN running over a shared NAT cloud (simulating the internet).

### Site Firewall Summary

| Site | Firewall | WAN IP (DHCP) | LAN | DMZ |
|------|----------|----------------|-----|-----|
| Head Office | FW-HO | 192.168.122.229 | 10.0.1.0/24 | 10.0.2.0/24 |
| Data Centre 1 | FW-DC1 | 192.168.122.143 | 10.1.1.0/24 | 10.1.2.0/24 |
| Data Centre 2 | FW-DC2 | 192.168.122.6 | 10.2.1.0/24 | 10.2.2.0/24 |
| **Maynooth (my site)** | **FW-MY** | **192.168.122.26** | **10.39.1.0/24** | **10.39.2.0/24** |

### Interface Roles

- **WAN (port1)** — DHCP from GNS3 NAT cloud; allows ping, HTTPS, HTTP, SSH for management
- **LAN (port2)** — static IP at `.10` of each LAN subnet; NAT applied on outbound traffic
- **DMZ (port3)** — static IP at `.1` of each DMZ subnet; isolates hosted services from the internal LAN

### VPN Architecture

Twelve IPsec site-to-site tunnels in total (three per firewall), forming six unique site pairs in a full mesh. All tunnels configured via the FortiGate IPsec Wizard with a shared pre-shared key, no NAT between sites.

### Remote Access Design

**Mobile staff** connect via FortiClient SSL VPN, authenticating against port1 and placed into a dedicated VPN IP pool. Firewall policies control access to internal resources. **Maintenance contractors** use a restricted SSL VPN profile that routes only to the DMZ, with a separate user group and time-limited policy enforcing LAN separation.

### Tests Conducted

1. **Interface Verification** — Confirmed correct IPs, aliases, and roles on all four firewalls via `show system interface`.
2. **Firewall Address Objects** — Confirmed `InsideLan` object present on each firewall with correct subnet.
3. **Firewall Policies** — Confirmed policy ID 1 (Inside→Outside) with NAT enabled on all firewalls.
4. **LAN-to-WAN Connectivity** — Client100 (HO LAN) and Client200 (MY LAN) both reached their respective firewall LAN gateways with 0% packet loss.
5. **VPN Status** — All 12 tunnels brought up; green status confirmed in the FortiGate GUI.
6. **Cross-Site Ping** — Pinged FW-MY LAN (`10.39.1.100`) from Client100 (`10.0.1.100`, HO LAN) successfully, confirming the VPN-HO-to-MY tunnel passes traffic end-to-end.

### Deliverables

- FortiGate config diffs per firewall (`diffs/`)
- FortiGate GUI screenshots (`fortigate_screenshots/`)
- Network topology and design diagrams

---

## Design Standards

- Structured cabling best practices
- Fibre backbone between buildings
- Layered design methodology
- VLAN segmentation for security
- Centralised rack containment
- Industry documentation standards

---

## Technologies Used

| Category | Technology |
|---|---|
| Physical Layer | Structured Cabling Design, Physical Containment Planning |
| Logical Layer | VLAN Architecture, Cisco-style Switch Configuration |
| WAN Routing | OSPF Multi-Area Routing, ABR/IR Design, Loopback Interfaces |
| Firewall & Security | FortiGate 6.4, IPsec Site-to-Site VPN, DMZ Design, SSL VPN, NAT Policies |
| Documentation | Network Wirelists, Bill of Materials |
| Simulation | Azure Lab, GNS3 |

---

## Key Learning Outcomes

- Real-world network design workflow
- Industry documentation practices
- Physical-to-logical design mapping
- Rack and containment planning
- Structured VLAN segmentation
- Prototype network implementation
- OSPF multi-area WAN design and configuration
- ABR and internal router roles in hierarchical routing
- FortiGate firewall deployment and interface configuration
- Full-mesh IPsec VPN architecture across multiple sites
- DMZ design and remote access security (SSL VPN, contractor isolation)