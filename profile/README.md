# Pale Blue Systems Foundation

The Pale Blue Systems Foundation (PBSF) stewards the Pale Blue Systems (PBS) Open Standard. PBS is an application-layer protocol that carries mission semantics between mission applications independently of the transport beneath it, including the IP and Bundle Protocol Version 7 (BPv7) network services of LunaNet. The semantics include priority, Service Intent, authority, authentication, and position, navigation and timing (PNT) context.

PBSF publishes the PBS Core specifications, reviews and accepts changes, manages versioning and deprecation, and maintains conformance guidance. It does not develop mission-specific software, operate networks or deploy infrastructure (PBS-GOV-01 Section 3.1). Under [PBS-GOV-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-GOV-01.md) Section 3.2, Pale Blue Systems is a commercial entity that may build proprietary implementations of PBS Core, offer PBS-compatible products, services and infrastructure, and contribute proposals and reference implementations under PBSF governance; it has no special authority over PBS Core beyond that of any other contributor.

---

## Engineering Problem

LunaNet is the lunar communications and PNT interoperability framework that NASA, ESA and JAXA define in the [LunaNet Interoperability Specification, Version 5](https://www.nasa.gov/wp-content/uploads/2025/02/lunanet-interoperability-specification-v5-baseline.pdf) (LNIS V005, baseline, 29 January 2025):

- No single LunaNet Service Provider (LNSP) has to meet every user need. LNIS expects users to be served by a combination of interoperable LNSPs (Section 1).
- Real-time IP network services carry traffic when source and destination are both on an IP-capable part of the network (Section 3.1.1.2).
- BPv7 carries traffic over links with disruption or delay, or where no robust end-to-end path exists (Section 3.1.2).

NASA's [Moon to Mars Architecture Definition Document](https://www.nasa.gov/wp-content/uploads/2025/12/add-revision-c-20251211.pdf) (ESDMD-001 Revision C, 12 December 2025), Section 2.3.14.2, states: "NASA seeks to empower network users with a long-term, scalable, and interoperable C&PNT architecture." The same section names LNIS as the structure of standards, protocols and interface requirements for LunaNet, and states that NASA must define, adopt and implement lunar reference systems, including reference frames, in the early stages of architecture development.

A message between two lunar assets can therefore cross more than one provider, over IP or over BPv7. LNIS defines the standards and interfaces with which providers deliver interoperable services (Section 1.1). PBS defines the application-layer fields the receiving application acts on: the sender's identity (Source ID), the message priority and deadline, the commanding authority, and the reference frame and time reference of PNT data. [PBS-LNIS-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-LNIS-01.md) requires every provider transition to preserve the PBS Source ID, authority context, priority, Service Intent and protected application payload (PBS-LNIS-REQ-007).

---

## NASA FY26 Civil Space Shortfalls

NASA's Space Technology Mission Directorate (STMD) defines a shortfall as "a technology area requiring further development to meet future exploration, science, and other mission needs" ([FY26 Civil Space Shortfall Prioritization](https://www.nasa.gov/wp-content/uploads/2026/05/fy26-civil-space-shortfall-prioritization.pdf), May 2026, p. 3). The FY26 prioritization consolidates the 187 shortfalls STMD published in 2024 into 32 categories, and each category contains numbered need statements. PBS v1.4 traces its requirements to four need statements:

| Need | NASA need statement | PBS requirements | Implementing specifications |
| --- | --- | --- | --- |
| 13.09 | "Provide advanced networking needed for multi-spacecraft responsive space operations." | PBS-NASA-1309-001 to -003 | PBS-SVC-01, PBS-PRIO-01, PBS-QOS-MAP-01, PBS-CAPS-01 |
| 15.01 | "Provide scalable, reliable surface-to-surface communications between assets on the lunar surface that is usable by all participating elements." | PBS-NASA-1501-001 to -003 | PBS-ENV-01, PBS-SVC-01, PBS-LNIS-01, PBS-DTN-MAP-02, PBS-CONFORMANCE-02 |
| 15.03 | "Achieve safe, efficient human-robot interactions for exploration missions, secure command and control over high-latency, bandwidth-limited networks, or implement reliable automated safing sequences." | PBS-NASA-1503-001 to -005 | PBS-AUTH-01, PBS-SEC-B-01, PBS-SVC-01, PBS-CONFORMANCE-02 |
| 24.05 | "Develop a lunar position, navigation, and timing architecture capable of scaling to long term operational needs." | PBS-NASA-2405-001 to -003 | PBS-PNT-CTX-01 |

STMD lists 13.09, 15.01 and 24.05 among its 40 primary focus areas for FY26 (pp. 10–11).

The traceability matrix [PBS-TRACE-NASA-FY26-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-ALIGNMENT-LIB/PBS-TRACE-NASA-FY26-01.md) also traces PBS-LNIS-001 to -003 to LNIS V005, and PBS-BPV7-001 and -002 to RFC 9171 / CCSDS. It assigns each requirement one or two verification methods from analysis (A), inspection (I), demonstration (D) and test (T). The matrix is a PBS engineering record, not a NASA document. No verification results against it are published.

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

- PBS Core conformance requires [PBS-ENV-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-ENV-01.md) v1.3, PBS-PRIO-01 v1.4 and [PBS-SEC-A-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-SEC-A-01.md) v1.3 ([PBS-CONFORMANCE-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-CONFORMANCE-01.md) Section 3). PBS-ENV-01 defines a fixed 44-byte big-endian header followed by the payload. The header CRC-32 (IEEE 802.3) covers header bytes 0x00–0x2B with the CRC32 field (0x28–0x2B) set to zero; it does not cover the payload.
- [PBS-PRIO-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-PRIO-01.md) defines five priority classes: 0 CRITICAL, 1 HIGH, 2 NORMAL, 3 LOW, 4 BULK. Values 5–255 are reserved, and receivers discard envelopes that carry them (Section 5.1).
- PBS-LNIS-01 requires an implementation to support a BPv7 binding when the mission profile requires disruption-tolerant service (PBS-LNIS-REQ-002), and permits IP bindings for contemporaneous connectivity (PBS-LNIS-REQ-003).
- [PBS-DTN-MAP-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-DTN-MAP-01.md) (v1.3) maps each envelope to exactly one bundle and places the complete envelope, header and payload, in a single BPv7 payload block (Sections 5.1, 6.2). [PBS-DTN-MAP-02](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-DTN-MAP-02.md) (v1.4) bounds the bundle lifetime so that network delivery cannot extend a message beyond its PBS deadline or expiry (Section 4).
- Contact plans, route computation and provider path selection are DTN and network-service functions. PBS Service Intent supplies application requirements as policy input to them (PBS-DTN-MAP-02 Section 8).

---

## Current Release

PBS v1.4.1 (2026-10-06) is the current release. It is an errata and documentation release of PBS v1.4 (2026-09-22) and does not change the wire format. Its errata correct normative text in PBS-ENV-01, PBS-SEC-A-01, PBS-CONFORMANCE-01, PBS-PRIO-01, PBS-ROUTE-01, PBS-ADDR-01, PBS-MUX-01, PBS-CAPS-01, PBS-POS-01, PBS-SEC-B-01 and PBS-CONFORMANCE-02. They add Traceability sections to PBS-ENV-01 (Section 21), PBS-PRIO-01 (Section 15) and PBS-CAPS-01 (Section 15), complete those of PBS-SVC-01 (Section 13) and PBS-CONFORMANCE-02 (Section 6), and reconcile the Allocation column of PBS-TRACE-NASA-FY26-01 with the specification Traceability sections.

PBS-ENV-01 Section 4, PBS-SEC-A-01 Sections 4.1 and 5.1 and PBS-CONFORMANCE-01 Sections 4.3 and 5.1 stated the header CRC-32 coverage as bytes 0x00–0x27. They now state bytes 0x00–0x2B with the CRC32 field zeroed, the rule PBS-ENV-01 Section 13 already specified. The PBS-ENV-01 Section 13.2 test vector has CRC32 0x588721ED; the superseded rule yields 0x019507AC. PBS-ENV-01 Section 12.2 stated that the TTL expiry check takes the Timestamp field in Unix epoch seconds. It now states microseconds, the unit Section 10 defines and the expiry formula already assumed.

PBS v1.4, the NASA FY26 / LunaNet alignment release, added mission Service Intent (PBS-SVC-01), authority and scope context (PBS-AUTH-01), authenticated mission messaging (PBS-SEC-B-01), PNT context (PBS-PNT-CTX-01), the LunaNet application alignment profile (PBS-LNIS-01), the BPv7 mapping PBS-DTN-MAP-02, mission-intent-to-network-treatment mapping (PBS-QOS-MAP-01), the NASA/LunaNet conformance and verification profile (PBS-CONFORMANCE-02), the FY26 alignment assignment (PBS-ALIGN-ASSIGNMENT-NASA-FY26-01), the traceability matrix PBS-TRACE-NASA-FY26-01 and the architecture mapping PBS-ALIGN-NASA-LCRNS-02.

The [changelog](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-PROTOCOL-CHANGELOG.md) records the errata and additions of each release.

---

## Repositories

| Repository | Content |
| --- | --- |
| [PBS-PROTOCOL-OPEN](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN) | PBS specifications (`PBS-RFC-LIB/`), governance, changelog, and alignment and traceability records (`PBS-ALIGNMENT-LIB/`). |
| [PBS_LINK](https://github.com/Pale-Blue-Systems/PBS_LINK) | Python reference SDK that builds and parses PBS-ENV-01 v1.3 envelopes; pip distribution `pbs-link` 0.1.1, import package `PBS_LINK`. |
| [PBS-EDGE-ADAPTER-MV](https://github.com/Pale-Blue-Systems/PBS-EDGE-ADAPTER-MV) | Reference design and tested Python worked example that builds a BPv7 bundle (RFC 9171) carrying one PBS-ENV-01 envelope in its payload block; it does not connect to a bundle protocol agent. |
| [PBS-APPLICATION-LAYER-RISK-MANAGMENT](https://github.com/Pale-Blue-Systems/PBS-APPLICATION-LAYER-RISK-MANAGMENT) | Python admission-control governors that refuse outbound packets by PBS-PRIO-01 class, lowest class first, as a 24-hour data-volume or transmit-energy budget depletes; the transmit-energy governor also refuses every class except CRITICAL while battery charge is below a configured cutoff. CRITICAL (0) is always admitted. |

None of these repositories implements the v1.4 extensions PBS-SVC-01, PBS-AUTH-01, PBS-SEC-B-01 or PBS-PNT-CTX-01.

---

## Licensing and Governance

All four repositories are licensed under the Apache License 2.0. Changes to PBS Core follow the RFC process in [PBS-GOV-01](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/PBS-RFC-LIB/PBS-GOV-01.md) Section 5 and the versioning policy in Section 6. Submitting a contribution to PBS-PROTOCOL-OPEN accepts the PBSF [Contributor License Agreement](https://github.com/Pale-Blue-Systems/PBS-PROTOCOL-OPEN/blob/main/CLA.md) (CLA Section 1).
