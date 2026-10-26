# CCNA + CCNA Automation — Weeks 1–16

**Course format:** 2 hours live per week · 16 weeks · 32 live instructional hours  
**Audience:** Beginners through experienced technologists · 150+ enrolled  
**Goal:** Build traditional CCNA fundamentals while gradually introducing automation as an alternative way to describe, inspect, validate, and eventually provision networks.

> **Guiding principle:** Understand and verify the network manually before automating it. Network requirements and acceptance criteria are the same for both paths.

## Instructional allocation

- **Networking:** 1,540 minutes (80.2%)
- **Automation:** 380 minutes (19.8%)
- **Total:** 1,920 minutes (32 hours)

The percentages refer to **live instructional time**, not Cisco's certification exam blueprint weights. Independent labs and reading are additional. Early automation is primarily **validation and configuration generation**, not direct device deployment.

## 16-week schedule

| Week | Core networking lesson | Gradual automation integration | Live automation time |
|---|---|---|---:|
| 1 | What is a network? OSI, TCP/IP, Ethernet | None; verify Lab 000 software readiness | 0 min |
| 2 | MAC addresses, ARP, ICMP, Wireshark | None; observe frames and packets | 0 min |
| 3 | IPv4 addresses and subnet masks | First Python `ipaddress` demonstration | 10 min |
| 4 | Subnetting, gateways, binary | Python subnet membership checks | 10 min |
| 5 | Switching, MAC tables, ports | Represent devices/interfaces in JSON inventory | 15 min |
| 6 | VLANs and access ports | JSON/YAML as structured network data | 15 min |
| 7 | Trunks, VLAN tagging, basic STP | Git: clone, add, commit, diff | 20 min |
| 8 | Inter-VLAN routing | Generate IOS configuration snippets with Python | 20 min |
| 9 | Router interfaces and routing tables | Parse saved CLI output | 25 min |
| 10 | Static routing and default routes | Validate expected routes in Python | 25 min |
| 11 | IPv6 addressing and routing basics | Reusable Python functions and input validation | 30 min |
| 12 | DHCP, DNS, NAT fundamentals | HTTP, REST, and JSON responses using mock data | 35 min |
| 13 | ACL fundamentals and security | Python tests for expected network policy | 40 min |
| 14 | OSPF fundamentals | Ansible inventory and read-only network commands | 45 min |
| 15 | OSPF troubleshooting and verification | Compare CLI output with automated state checks | 45 min |
| 16 | Integrated routing and switching challenge | Dual-path configuration and validation | 45 min |
| **Total** | | | **380 min** |

## Weekly labs and optional extensions

All students complete the **core lab**. Optional challenges are intended for advanced students or students pursuing the CCNA Automation path. Lab titles are *suggested original assignments*, not chapter or exercise numbers from a published book.

| Week | Core lab (Packet Tracer unless otherwise specified) | Optional automation / extension |
|---|---|---|
| 1 | **LAB-001:** Connect two PCs through a switch; assign IPs; verify ping | Produce a simple topology diagram and device list |
| 2 | **LAB-002:** Trace ARP and ICMP in Packet Tracer Simulation Mode; capture local traffic in Wireshark | Annotate a packet trace with source/destination MAC and IP addresses |
| 3 | **LAB-003:** Configure hosts on the same and different /24 networks; predict reachability | Validate IP/network membership with `ipaddress` |
| 4 | **LAB-004:** Design /25, /26, /27 subnets; assign gateways; prove reachability | Read a CSV of addresses; flag incorrect subnet assignments |
| 5 | **LAB-005:** Connect multiple switches and clients; inspect MAC-address learning | Build a JSON device-and-interface inventory |
| 6 | **LAB-006:** Configure VLAN 10/20/30 and access ports; test isolation | Represent VLAN intent in YAML and validate IDs/names |
| 7 | **LAB-007:** Configure trunks; observe VLAN tagging; explore a redundant link/STP | Commit topology, screenshots, and sanitized configs to Git |
| 8 | **LAB-008:** Configure router-on-a-stick inter-VLAN routing and basic verification | Generate VLAN and subinterface configuration text from YAML; manually apply in Packet Tracer |
| 9 | **LAB-009:** Configure routed interfaces; interpret connected routes | Parse **saved** `show ip route` and `show ip interface brief` text |
| 10 | **LAB-010:** Connect three routers using static/default routes; deliberately break a next hop | Compare a saved route table against expected prefixes |
| 11 | **LAB-011:** Configure IPv6 addresses and basic IPv6 routing; verify neighbor discovery | Extend IP validation to IPv6 |
| 12 | **LAB-012:** Configure DHCP, DNS and NAT/PAT in a small branch network | Retrieve and inspect JSON from a local mock HTTP API |
| 13 | **LAB-013:** Apply a standard/extended ACL; verify permitted and denied flows | Express expected ACL behavior as test cases; generate a PASS/FAIL report |
| 14 | **LAB-014:** Configure single-area OSPF on three routers and verify neighbor relationships | Create Ansible inventory; use read-only commands against a **supported** IOS XE lab target or supplied sample outputs |
| 15 | **LAB-015:** Diagnose OSPF neighbor, network, or routing faults | Parse actual captured CLI output; flag missing neighbors/routes |
| 16 | **LAB-016:** Capstone: multi-VLAN, three-router network with routing, ACLs and injected faults | Generate selected configuration artifacts and run automated checks; provide manual proof of functionality |

### Suggested lab submission standard

Each weekly submission should contain:

1. **Topology:** Packet Tracer `.pkt` file (when used), or topology diagram.
2. **Requirement checklist:** What was supposed to work and what was supposed to be blocked.
3. **Verification:** Relevant `show` output, ping/traceroute results, or packet captures.
4. **Failure exercise:** One fault, diagnosis, corrective action, and retest.
5. **Automation (when assigned):** Script/data files, sample output, and a short explanation of what the script can and cannot prove.

The class may use team repositories for collaboration, but students should submit individual evidence of understanding for readiness decisions.

## Delivery guardrails

- **Packet Tracer is the default networking lab.** It does not provide a full Cisco IOS XE RESTCONF/NETCONF/Ansible automation target. Initially generate CLI text and apply it manually.
- **Wireshark inspects actual local traffic;** Packet Tracer Simulation Mode illustrates simulated packet flow. The observations are complementary, not interchangeable.
- **API exercises initially use mock/local data.** A Cisco DevNet sandbox can be an optional extension when availability and access are verified.
- **Ansible requires a suitable supported device or emulator** for real network-command execution; a local inventory and provided output files can serve as the fallback.
- **No credentials in Git.** Use example configuration and sanitized outputs.
- **The published CCNA and DevNet/CCNA Automation books are references.** Match their chapters and Packet Tracer labs to the week by topic after reviewing the actual editions; do not assume that a book's lab numbering corresponds to this syllabus.

## Week 16 readiness gate

**Proposed assessment weighting:**

- 50% — networking concepts and troubleshooting
- 30% — functioning implementation (manual or automation-assisted)
- 20% — verification, testing, and documentation

All students must show both manual networking competence and introductory automation literacy. The optional automation path adds depth; it does not excuse core networking requirements.

## Beyond Week 16

In Weeks 17–32, progressively expand supported device APIs, Ansible, NETCONF/RESTCONF/YANG, reliable device-state collection, and network-as-code workflows. Introduce Terraform where a suitable provider and actual infrastructure use case justify it. Full enterprise SD-WAN deployment belongs primarily in the later CCNP track.
