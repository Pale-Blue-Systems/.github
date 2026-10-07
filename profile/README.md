# Pale Blue Systems Foundation

The **Pale Blue Systems Foundation (PBSF)** is an independent, foundation-led steward of **open standards and reference implementations** for reliable, interoperable communication across **space, lunar, planetary, and other extreme or delay-tolerant environments**.

PBSF exists to ensure that spacecraft, rovers, habitats, autonomous systems, and ground infrastructure can **communicate, coordinate, and exchange data safely and predictably** across heterogeneous networks where traditional terrestrial assumptions—continuous connectivity, low latency, single-authority control—do not apply.

The Foundation provides the **shared technical language and governance layer** that allows civil, commercial, and international space systems to interoperate without requiring shared vendors, shared hardware, or proprietary disclosure.

The Pale Blue Systems Foundation (PBSF) stewards the Pale Blue Systems (PBS) Open Standard. PBS is an application-layer protocol that carries mission semantics between mission applications independently of the transport beneath it, including the IP and Bundle Protocol Version 7 (BPv7) network services of LunaNet. The semantics include priority, Service Intent, authority, authentication, and position, navigation and timing (PNT) context.

PBSF publishes the PBS Core specifications, reviews and accepts changes, manages versioning and deprecation, and maintains conformance guidance. It does not develop mission-specific software, operate networks or deploy infrastructure (PBS-GOV-01 Section 3.1). Under [PBS-GOV-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-GOV-01.md) Section 3.2, Pale Blue Systems is a commercial entity that may build proprietary implementations of PBS Core, offer PBS-compatible products, services and infrastructure, and contribute proposals and reference implementations under PBSF governance; it has no special authority over PBS Core beyond that of any other contributor.

---

## Why the Foundation Exists

As space operations move toward sustained lunar presence, cislunar infrastructure, and Mars exploration, missions increasingly depend on **distributed, networked systems** operating across:

- long and variable communication delays
- intermittent or scheduled connectivity
- multiple independent authorities and vendors
- human-rated, life- and safety-critical environments

These conditions require communication architectures that are **store-and-forward by design**, tolerant of disruption, and interoperable across organizational boundaries.

---

## Engineering Problem

LunaNet is the lunar communications and PNT interoperability framework that NASA, ESA and JAXA define in the [LunaNet Interoperability Specification, Version 5](https://www.nasa.gov/wp-content/uploads/2025/02/lunanet-interoperability-specification-v5-baseline.pdf) (LNIS V005, baseline, 29 January 2025):

- No single LunaNet Service Provider (LNSP) has to meet every user need. LNIS expects users to be served by a combination of interoperable LNSPs (Section 1).
- Real-time IP network services carry traffic when source and destination are both on an IP-capable part of the network (Section 3.1.1.2).
- BPv7 carries traffic over links with disruption or delay, or where no robust end-to-end path exists (Section 3.1.2).

In parallel, NASA’s **Moon to Mars Architecture Definition Document** describes an exploration strategy that explicitly depends on **interoperable, extensible, and evolvable communications and data systems** spanning Earth, lunar, and Mars domains.

NASA's [Moon to Mars Architecture Definition Document](https://www.nasa.gov/wp-content/uploads/2025/12/add-revision-c-20251211.pdf) (ESDMD-001 Revision C, 12 December 2025), Section 2.3.14.2, states: "NASA seeks to empower network users with a long-term, scalable, and interoperable C&PNT architecture." The same section names LNIS as the structure of standards, protocols and interface requirements for LunaNet, and states that NASA must define, adopt and implement lunar reference systems, including reference frames, in the early stages of architecture development.

A message between two lunar assets can therefore cross more than one provider, over IP or over BPv7. LNIS defines the standards and interfaces with which providers deliver interoperable services (Section 1.1). PBS defines the application-layer fields the receiving application acts on: the sender's identity (Source ID), the message priority and deadline, the commanding authority, and the reference frame and time reference of PNT data. [PBS-LNIS-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-LNIS-01.md) requires every provider transition to preserve the PBS Source ID, authority context, priority, Service Intent and protected application payload (PBS-LNIS-REQ-007).

---

## NASA FY26 Civil Space Shortfalls

NASA’s Space Technology Mission Directorate (STMD) has formally identified **communications, networking, and coordination** as critical technology shortfalls that must be addressed to support future exploration architectures.

NASA's Space Technology Mission Directorate (STMD) defines a shortfall as "a technology area requiring further development to meet future exploration, science, and other mission needs" ([FY26 Civil Space Shortfall Prioritization](https://www.nasa.gov/wp-content/uploads/2026/05/fy26-civil-space-shortfall-prioritization.pdf), May 2026, p. 3). The FY26 prioritization consolidates the 187 shortfalls STMD published in 2024 into 32 categories, and each category contains numbered need statements. The PBS traceability matrix, added in PBS v1.4 and unchanged in v1.5.0, traces PBS requirements to four need statements:

| Need | NASA need statement | PBS requirements | Implementing specifications |
| --- | --- | --- | --- |
| 13.09 | "Provide advanced networking needed for multi-spacecraft responsive space operations." | PBS-NASA-1309-001 to -003 | PBS-SVC-01, PBS-PRIO-01, PBS-QOS-MAP-01, PBS-CAPS-01 |
| 15.01 | "Provide scalable, reliable surface-to-surface communications between assets on the lunar surface that is usable by all participating elements." | PBS-NASA-1501-001 to -003 | PBS-ENV-01, PBS-SVC-01, PBS-LNIS-01, PBS-DTN-MAP-02, PBS-CONFORMANCE-02 |
| 15.03 | "Achieve safe, efficient human-robot interactions for exploration missions, secure command and control over high-latency, bandwidth-limited networks, or implement reliable automated safing sequences." | PBS-NASA-1503-001 to -005 | PBS-AUTH-01, PBS-SEC-B-01, PBS-SVC-01, PBS-CONFORMANCE-02 |
| 24.05 | "Develop a lunar position, navigation, and timing architecture capable of scaling to long term operational needs." | PBS-NASA-2405-001 to -003 | PBS-PNT-CTX-01 |

STMD lists 13.09, 15.01 and 24.05 among its 40 primary focus areas for FY26 (pp. 10–11).

NASA’s shortfall process highlights the need for advances in areas including high-rate space communications, autonomous operations, and distributed systems that must function reliably across deep space and planetary environments.

Together, these documents make clear that future missions require **shared networking standards** capable of operating across long distances, disconnected environments, and diverse mission operators.

The traceability matrix [PBS-TRACE-NASA-FY26-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-ALIGNMENT-LIB/PBS-TRACE-NASA-FY26-01.md) also traces PBS-LNIS-001 to -003 to LNIS V005, and PBS-BPV7-001 and -002 to RFC 9171 / CCSDS. It assigns each requirement one or two verification methods from analysis (A), inspection (I), demonstration (D) and test (T). The matrix is a PBS engineering record, not a NASA document. No verification results against it are published.

---

## How Pale Blue Systems Addresses This Problem (Planned Architecture)

PBSF directly addresses these NASA-identified needs by stewarding **open standards and reference implementations** that sit **between space hardware and mission applications**, enabling interoperability without constraining innovation.

### Architectural Commitments (design targets)

The standards stewarded by PBSF are designed to:

- **Align with NASA’s Delay/Disruption Tolerant Networking (DTN) architecture**, including compatibility with CCSDS and Internet Bundle Protocol concepts
- **Prioritize store-and-forward communication**, treating disconnection as normal rather than exceptional
- **Support data classification and prioritization**, ensuring that life- and safety-critical telemetry and command data are handled appropriately
- **Enable seamless communication between proprietary systems**, regardless of latency profile, vendor, or deployment context

PBSF standards are designed to **translate and interoperate with NASA-adopted DTN implementations**, including the **Interplanetary Overlay Network (ION)**.

ION demonstrates how DTN-based protocols can be deployed across flight and ground systems; PBSF builds on this foundation to enable **multi-party, multi-vendor interoperability** at scale.

---

## Where PBSF Fits (Planned Architecture Overview)

The Pale Blue Systems standards operate as **middleware**, abstracting communication complexity while remaining grounded in real space networking constraints.

```text
+------------------------------------------------------+
|                  Mission Applications                 |
|   (Rovers, Landers, Habitats, Drones, Ops Software)   |
+----------------------▲-------------------------------+
                       |
                       |  Interoperable Data Exchange
                       |
+----------------------|-------------------------------+
|        Pale Blue Systems Standards & Reference       |
|            Implementations (Middleware Layer)        |
|   - DTN-aligned messaging                            |
|   - Store-and-forward transport                      |
|   - Safety & priority handling                       |
|   - Multi-authority interoperability                 |
+----------------------▲-------------------------------+
                       |
                       |  Translated / Abstracted Links
                       |
+----------------------|-------------------------------+
|     Space Communication Hardware & Links             |
|   (Radios, Lasers, Relays, Ground Stations, Antennas)|
+------------------------------------------------------+
```

PBSF does **not** replace mission software or physical communication systems.
It provides the **common protocol language** that allows them to work together.

---

## Where PBS Sits

```text
+---------------------------------------------------------------------+
| Mission applications                                                |
| rovers, landers, habitats, robots, operations software              |
+---------------------------------------------------------------------+
| PBS mission semantics (application protocol data)                   |
|   Core:     PBS-ENV-01 envelope, PBS-PRIO-01 priority,              |
|             PBS-SEC-A-01 header integrity                           |
|   v1.4:     PBS-SVC-01 Service Intent, PBS-AUTH-01 authority,       |
|             PBS-SEC-B-01 authentication, PBS-PNT-CTX-01 PNT context |
|   Mappings: PBS-LNIS-01, PBS-DTN-MAP-01, PBS-DTN-MAP-02,            |
|             PBS-QOS-MAP-01                                          |
+---------------------------------------------------------------------+
| Network services (LunaNet and other IP and DTN networks)            |
|   real-time IP  |  BPv7 (RFC 9171) with BPSec (RFC 9172)            |
+---------------------------------------------------------------------+
| Providers and links                                                 |
| LNSPs, relays, ground stations; RF, optical, 3GPP, Wi-Fi, wired     |
+---------------------------------------------------------------------+
```

- PBS Core conformance requires [PBS-ENV-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-ENV-01.md) v1.5, PBS-PRIO-01 v1.4 and [PBS-SEC-A-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-SEC-A-01.md) v1.5 ([PBS-CONFORMANCE-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-CONFORMANCE-01.md) Section 3) and the further MUST requirements of PBS-CONFORMANCE-01 Sections 4–9 and 12. PBS-ENV-01 defines a fixed 44-byte big-endian header followed by the payload. The header CRC-32 (IEEE 802.3) covers header bytes 0x00–0x2B with the CRC32 field (0x28–0x2B) set to zero; it does not cover the payload.
- [PBS-PRIO-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-PRIO-01.md) defines five priority classes: 0 CRITICAL, 1 HIGH, 2 NORMAL, 3 LOW, 4 BULK. Values 5–255 are reserved, and receivers discard envelopes that carry them (Section 5.1).
- PBS-LNIS-01 requires an implementation to support a BPv7 binding when the mission profile requires disruption-tolerant service (PBS-LNIS-REQ-002), and permits IP bindings for contemporaneous connectivity (PBS-LNIS-REQ-003).
- [PBS-DTN-MAP-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-DTN-MAP-01.md) (v1.5) maps each envelope to exactly one bundle and places the complete envelope, header and payload, in a single BPv7 payload block (Sections 5.1, 6.2). [PBS-DTN-MAP-02](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-DTN-MAP-02.md) (v1.5) bounds the bundle lifetime so that network delivery cannot extend a message beyond its PBS deadline or expiry (Section 4).
- Contact plans, route computation and provider path selection are DTN and network-service functions. PBS Service Intent supplies application requirements as policy input to them (PBS-DTN-MAP-02 Section 8).

---

## Benefits for Commercial and Civil Space Systems (Concept of Operations)

A commercial spacecraft, rover, habitat, drone, or field technician benefits from PBSF standards by gaining:

- Interoperability with NASA and other civil programs without bespoke integration
- Compatibility across high-latency and low-latency networks using a single logical model
- Reduced engineering risk through alignment with NASA-recognized architectures
- Freedom to innovate internally while communicating externally through shared standards

This lowers integration cost, reduces mission risk, and enables participation in multi-party exploration architectures.

---

## Why Open Standards and Neutral Stewardship Matter

PBSF is intentionally structured as a **neutral foundation** stewarding **open standards and reference implementations**:

- **Open standards enable trust and adoption** across agencies, companies, and nations
- **Reference implementations provide clarity**, not commercial lock-in
- **Neutral governance ensures longevity**, allowing the standards to outlive individual missions or vendors

This mirrors the model that allowed the Internet to scale globally—and applies it to the far more constrained domain of space.

---

## Current Release

PBS v1.5.0 (2026-10-06) is the current release. It resolves the six known issues recorded in PBS v1.4.1 and does not change the wire format: Magic `0x10`, the 44-byte header and every field encoding are unchanged. It is a corrective release (PBS-GOV-01 Section 5.2), released as a minor version because no clause of v1.4.1 stated the controlling rule (PBS-GOV-01 Section 6).

TTL and relaying:

- TTL is the lifetime of the envelope counted from Timestamp. The originator sets it; relays and gateways do not modify it (PBS-ENV-01 Sections 12.1 and 15). The decrement-based method of PBS-ENV-01 Section 12.3 is removed.
- Relays and gateways apply the PBS-ENV-01 Section 12.2 expiry check against the unchanged Timestamp and TTL and forward the 44 header bytes as received, TTL and CRC32 included, so every node verifies the CRC-32 the originator computed (PBS-ENV-01 Section 12.3; PBS-SEC-A-01 Section 5.1). They maintain a clock synchronized to Unix epoch time (PBS-ENV-01 Section 15).
- An envelope with TTL `0` is never discarded as TTL-expired (PBS-ENV-01 Section 12.1). PBS-ROUTE-01 Section 10 recommends an additional loop-detection mechanism for these envelopes, with duplicate-suppression state kept only for a configured interval.
- PBS-CONFORMANCE-01 Sections 5.2 and 8 and PBS-ROUTE-01 Section 12 state the same relay and gateway rules. PBS-SEC-B-01 Section 5 states that PBS-ENV-01 header fields, TTL included, are not mutable network-layer fields.

BPv7 mapping (PBS-DTN-MAP-01 v1.5, PBS-DTN-MAP-02 v1.5):

- For TTL > 0 the bundle lifetime does not exceed the time remaining until the envelope expires, and an envelope with less than 1 ms remaining is not encapsulated (PBS-DTN-MAP-01 Section 6.1).
- For TTL `0`, where no finite deadline, maximum age or mission expiry limit applies, the gateway or adapter sets a documented no-expiry lifetime: greater than 0 ms, not less than any other lifetime it assigns, at most `4294967295000` ms, and without overflow in the expiration time its bundle protocol agent computes (PBS-DTN-MAP-01 Section 6.1.1; PBS-DTN-MAP-02 Section 4).
- The gateway's bundle protocol agent assigns the bundle creation timestamp. The sequence number is not derived from the PBS `Sequence` field (PBS-DTN-MAP-01 Section 6.1; RFC 9171 Section 4.2.7).
- No primary block field carries PBS priority, and gateways do not set reserved or unassigned bundle processing control flags to convey it. A gateway that requests network treatment on the basis of priority documents a PBS-DTN-MAP-02 Section 5 mapping profile that covers all five priority classes and, when all other inputs to the mapping are equal, requests no more favorable treatment for a class than for any higher-priority class. Where it requests the Expedited, Normal and Bulk classes of RFC 4838 Section 3.5, CRITICAL and HIGH map to Expedited, NORMAL to Normal, and LOW and BULK to Bulk (PBS-DTN-MAP-01 Section 6.3).
- [PBS-CONFORMANCE-02](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-CONFORMANCE-02.md) test PBS-C02-T002 requires the PBS-ENV-01 header to arrive byte-identical after BPv7 carriage, and test PBS-C02-T016 verifies the no-expiry lifetime.

Governance: PBS-GOV-01 Section 5.2 adds the Corrective category: changes to normative text that resolve a conflict between clauses, or with a normatively referenced standard, together with requirements that follow from that resolution, without changing the wire format. A corrective change that makes a permitted behavior non-conformant requires migration guidance. Section 6 releases a corrective change in a patch version when another clause of the preceding release states the controlling rule, and in a minor version otherwise. PBS-GOV-01 Section 6, PBS-CONFORMANCE-01 Section 12 and CONTRIBUTING Section 3 exclude corrective changes from the major-version rule. These governance amendments are Additive changes (PBS-GOV-01 Section 5.2).

PBS-ENV-01, PBS-SEC-A-01, PBS-CONFORMANCE-01, PBS-ROUTE-01, PBS-SEC-B-01, PBS-DTN-MAP-01, PBS-DTN-MAP-02, PBS-CONFORMANCE-02 and PBS-GOV-01 are at version 1.5. Each records its changes in a **Changes** line, which incorporates any PBS v1.4.1 errata. The other specifications keep version 1.3 or 1.4.

The [Migration](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-PROTOCOL-CHANGELOG.md#migration) section of the v1.5.0 changelog entry lists the changes for relays and gateways, PBS-DTN-MAP-01 gateways, PBS-DTN-MAP-02 adapters, and PBS-SEC-B-01 binding profiles that excluded TTL from the protected data. A receiver cannot detect a TTL reduced by a v1.4.1 decrement-based relay; until every such relay on a path is migrated, envelopes crossing it expire early and envelopes with TTL `0` are discarded there. Neither PBS_LINK nor the PBS Edge Adapter worked example decrements TTL.

One defect in normative text remains open ([Known issues](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-PROTOCOL-CHANGELOG.md#known-issues-not-corrected-in-v150)): PBS-DTN-MAP-01 Section 8 maps each Source ID to a source EID, and a mapping to the EID of a node other than the gateway produces bundles that do not conform to RFC 9171 Section 5.2, Step 1.

PBS v1.4.1 (2026-10-06) was an errata and documentation release of PBS v1.4 (2026-09-22) with no wire-format change. Its errata corrected normative text in PBS-ENV-01, PBS-SEC-A-01, PBS-CONFORMANCE-01, PBS-PRIO-01, PBS-ROUTE-01, PBS-ADDR-01, PBS-MUX-01, PBS-CAPS-01, PBS-POS-01, PBS-SEC-B-01 and PBS-CONFORMANCE-02. They added Traceability sections to PBS-ENV-01 (Section 21), PBS-PRIO-01 (Section 15) and PBS-CAPS-01 (Section 15), completed those of PBS-SVC-01 (Section 13) and PBS-CONFORMANCE-02 (Section 6), and reconciled the Allocation column of PBS-TRACE-NASA-FY26-01 with the specification Traceability sections. PBS-ENV-01 Section 4, PBS-SEC-A-01 Sections 4.1 and 5.1 and PBS-CONFORMANCE-01 Sections 4.3 and 5.1 had stated the header CRC-32 coverage as bytes 0x00–0x27; v1.4.1 corrected them to bytes 0x00–0x2B with the CRC32 field zeroed, the rule PBS-ENV-01 Section 13 already specified. The PBS-ENV-01 Section 13.2 test vector has CRC32 0x588721ED; the superseded rule yields 0x019507AC. v1.4.1 also corrected the Timestamp unit in the PBS-ENV-01 Section 12.2 expiry check from seconds to microseconds, the unit Section 10 defines.

PBS v1.4, the NASA FY26 / LunaNet alignment release, added mission Service Intent (PBS-SVC-01), authority and scope context (PBS-AUTH-01), authenticated mission messaging (PBS-SEC-B-01), PNT context (PBS-PNT-CTX-01), the LunaNet application alignment profile (PBS-LNIS-01), the BPv7 mapping PBS-DTN-MAP-02, mission-intent-to-network-treatment mapping (PBS-QOS-MAP-01), the NASA/LunaNet conformance and verification profile (PBS-CONFORMANCE-02), the FY26 alignment assignment (PBS-ALIGN-ASSIGNMENT-NASA-FY26-01), the traceability matrix PBS-TRACE-NASA-FY26-01 and the architecture mapping PBS-ALIGN-NASA-LCRNS-02.

The [changelog](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-PROTOCOL-CHANGELOG.md) records the changes, errata and migration guidance of each release.

---

## Repositories

| Repository | Content |
| --- | --- |
| [PBS-PROTOCOL-OPEN](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN) | PBS specifications (`PBS-RFC-LIB/`), governance, changelog, and alignment and traceability records (`PBS-ALIGNMENT-LIB/`). |
| [PBS_LINK](https://github.com/Pale-Blue-Systems/PBS_LINK) | Python reference SDK that builds and parses PBS-ENV-01 envelopes (the 44-byte header, unchanged since PBS-ENV-01 v1.3); pip distribution `pbs-link` 0.1.4, import package `PBS_LINK`. It is an endpoint library and does not forward envelopes. |
| [PBS-EDGE-ADAPTER-MV](https://github.com/Pale-Blue-Systems/PBS-EDGE-ADAPTER-MV) | Minimum viable reference for mapping PBS envelopes into BPv7 bundles at the network edge. Reference design and tested Python worked example that builds a BPv7 bundle (RFC 9171) carrying one PBS-ENV-01 envelope in its payload block; it does not connect to a bundle protocol agent. |
| [PBS-APPLICATION-LAYER-RISK-MANAGMENT](https://github.com/Pale-Blue-Systems/PBS-APPLICATION-LAYER-RISK-MANAGMENT) | Python admission-control governors that refuse outbound packets by PBS-PRIO-01 class, lowest class first, as a 24-hour data-volume or transmit-energy budget depletes; the transmit-energy governor also refuses every class except CRITICAL while battery charge is below a configured cutoff. CRITICAL (0) is always admitted. |

None of these repositories implements the v1.4 extensions PBS-SVC-01, PBS-AUTH-01, PBS-SEC-B-01 or PBS-PNT-CTX-01.

### Upstream DTN software

Pale Blue Systems does not fork or mirror third-party DTN software. Use the upstream repositories:

| Repository | Content |
| --- | --- |
| [nasa-jpl/ION-DTN](https://github.com/nasa-jpl/ION-DTN) | NASA/JPL Interplanetary Overlay Network (ION), an implementation of delay/disruption-tolerant networking. Its `bpv7` module implements RFC 9171 and is one bundle protocol agent that can carry PBS envelopes in BPv7 bundles. |
| [nasa-jpl/ion-config-tool](https://github.com/nasa-jpl/ion-config-tool) | JPL configuration tools that generate ION configuration files. |

---

## What You Will Find in This Repository (Roadmap)

- **Specifications** defining the Pale Blue Systems communication standards
- **Reference implementations** demonstrating correct, interoperable behavior
- **Conformance and interoperability tooling**
- **Governance artifacts** (RFCs, decision records, version history)

---

## Licensing and Governance

All four repositories are licensed under the Apache License 2.0. Changes to PBS Core follow the RFC process in [PBS-GOV-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-GOV-01.md) Section 5 and the versioning policy in Section 6. Submitting a contribution to PBS-PROTOCOL-OPEN accepts the PBSF [Contributor License Agreement](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/CLA.md) (CLA Section 1).

---

**Pale Blue Systems Foundation**
Stewarding open, interoperable communication standards for humanity’s expansion into space.
