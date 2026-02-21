# Electric Petrol Site Network Design

**Author:** Ayobami Pase  
**Project Type:** Industry-Style Network Infrastructure Design  
**Scope:** Layer 1 to Layer 2 Design and Prototype Implementation

---

## Overview

This project documents the full physical and logical network design for a greenfield **Electric Petrol Site** development. The site layout (minimum 400m × 200m) and building functions were agreed during initial client consultation, with preliminary floor plans provided for the forecourt building only.

This repository contains all Layer 1 and Layer 2 deliverables, including physical containment design, rack and cabinet placement, cable routing plans, wirelists, VLAN architecture, switch configuration sheets, logical diagrams, and prototype switch configurations.

> This project is structured and documented as an **industry deployment**, not an academic exercise.

---

## Client Background

**Client:** [electric-petrol.ie]

Electric Petrol is a startup operating in the emerging EV infrastructure space, responding to European legislation phasing out combustion engine vehicles by 2035. The business model centres on deploying service stations across the island of Ireland equipped with local electrical storage and generation capacity.

Sites leverage nearby wind and solar farms to charge graphene-based super-capacitors, minimising reliance on the national grid. Stored energy can also be sold back to the grid at peak times, creating an additional revenue stream.

The client had registered their domain but had no existing IT or network infrastructure. This project covers the full network design for one site, from physical containment through to logical configuration.

---

## Repository Structure

```
networking/
│
├── Layer 1/
│   ├── Site_Marked_Drawing.pdf
│   ├── Forecourt_Marked_Drawing.pdf
│   ├── BOM.xlsx
│   └── wirelist.xlsx
│
├── Layer 2/
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