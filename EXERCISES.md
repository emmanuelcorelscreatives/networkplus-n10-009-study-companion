# Written Exercises: Subnetting and Troubleshooting

Work independently before opening `ANSWER-GUIDE.md`. Write the objective, calculation or deciding evidence, the next action and how you would verify it. All addresses, counters and outputs below are fictional. The 192.0.2.0/24, 198.51.100.0/24 and 203.0.113.0/24 blocks are documentation examples, not public production allocations for your lab. No network access or equipment changes are required.

## Subnetting: six different decisions

### S1 — Locate the host, not just the mask (1.7)

A workstation is configured as 192.0.2.142/26. Calculate the dotted-decimal mask, network, broadcast, usable host range and usable host count. Is gateway 192.0.2.129 on the same subnet? Would 192.0.2.192 be another usable host in that subnet? Explain both decisions.

### S2 — Plan equal-size segments (1.7)

Split 198.51.100.0/24 into at least six equal-size LAN subnets, each supporting at least 25 addressed interfaces including its gateway. Use the smallest subnet size that meets the host requirement. Give the prefix, mask, number of subnets available and the network, usable range and broadcast of the third subnet when listed in ascending order starting with the zero subnet.

### S3 — Allocate unequal requirements (1.7)

Allocate 10.44.8.0/24 to four LANs requiring 100, 50, 20 and 10 usable addresses respectively; each number already includes gateways and other addressed interfaces. Allocate largest first, use the smallest fitting block for each and keep the plan contiguous from the start. Give every prefix, usable range and broadcast, then identify the remaining unused block.

### S4 — Check a proposed static address (1.7, 5.3)

A printer VLAN uses 203.0.113.64/28. The gateway is .65 and address management confirms .78 and .79 have no device assignments. A request proposes .79 for a new printer. Is it usable? Give an alternative from those two candidates and explain why checking only for duplicate assignments is insufficient. Assume the chosen usable address is reserved before installation.

### S5 — Work across an octet boundary (1.7, 2.1)

A host is 172.20.11.210/23. Give its mask, network, broadcast, usable range and host count. Which destination is on-link under that mask: 172.20.10.55 or 172.20.12.10? There are no more-specific routes, proxy ARP or alternative interfaces in this example. Explain where the host would send traffic for the off-link destination if a valid default gateway is configured.

### S6 — Detect an overlapping allocation (1.7, 3.1)

An address plan assigns 192.168.40.0/25 to Engineering and 192.168.40.64/26 to Voice. Both VLANs will be routed. Show the overlapping range, then propose the lowest-aligned nonoverlapping /26 within the same /24, assuming the rest of the /24 is unallocated. Give the corrected Voice usable range and broadcast. Explain why moving a gateway address alone does not fix the original plan.

## Troubleshooting: eight evidence-led decisions

### T1 — A client without its expected lease (3.4, 5.3, 5.5)

A DHCP-enabled workstation shows 169.254.22.9/16 and no default gateway. It is intended to use VLAN 30. A workstation on VLAN 20 obtains a normal lease from the same central DHCP server. The server has free VLAN 30 leases, and the failed client's switch port is correctly assigned to VLAN 30. VLAN 30 is routed elsewhere through a relay.

What does the observed address suggest? Choose a focused next investigation that can distinguish a relay/path problem from a dead DHCP server. Name the expected exchange evidence and the client state that would validate restoration. Do not assume the relay is faulty before checking it.

### T2 — Reachable service, inconsistent DNS (3.4, 5.3, 5.5)

A client's TCP connection to an internal test service at 192.0.2.20:8443 succeeds. Querying `files.example.test` with nslookup against the configured resolver 192.0.2.53 returns an old address; querying the authoritative server for the same name returns 192.0.2.20. The approved DNS change is recent. Other clients using 192.0.2.53 see the old address too.

Which boundary should you investigate first? What would you compare before changing anything? Explain why restarting the application or flushing only this client's cache is not yet a complete answer. State a verification that covers both name resolution and service access.

### T3 — One VLAN fails across a link (2.2, 5.3)

Two switches share an 802.1Q trunk. VLAN 10 crosses it successfully. The trunk's permitted-VLAN list is 10,20 on both ends. Access ports on both switches are assigned to VLAN 30, VLAN 30 exists on each switch and same-switch VLAN 30 hosts communicate. Cross-switch VLAN 30 hosts in the same IP subnet cannot communicate. Links are up and there are no rising physical error counters.

Identify the configuration boundary implicated by the evidence. Describe the narrow authorized change, a rollback and tests that show both restoration and preservation of the already-working service. Why is changing host default gateways not the first repair here?

### T4 — A controlled physical-path substitution (5.1, 5.2, 5.5)

A copper access link reports increasing CRC errors during a repeatable local file transfer. Negotiated speed and full-duplex settings match at both ends. With approval, a technician substitutes a tested patch lead while keeping the endpoint, switch port, configuration and workload unchanged. The CRC counter stops increasing and transfer throughput returns to baseline.

What does this comparison support, and what uncertainty remains? Describe the next validation and documentation steps. Explain why simultaneously moving the switch port and changing duplex settings would weaken the evidence.

### T5 — Strong signal, busy airtime (2.3, 5.4)

Conference-room clients show strong received signal, but video calls degrade during meetings. Measurements show high channel utilization and retries on the same 2.4 GHz channel used by nearby access points. A wired test from the same room to the same service is healthy. An authorized survey identifies a permitted 5 GHz channel with spare airtime, and the affected clients support that band.

Choose a bounded pilot action and the before/after measurements you would compare. Why is increasing transmit power on every AP not justified by these observations? Include what would trigger rollback rather than treating one good speed test as closure.

### T6 — Limit management without breaking the service (4.1, 4.3, 3.5)

In an AWS lab, an instance security group permits inbound TCP 22 from 0.0.0.0/0 and inbound TCP 443 from 0.0.0.0/0. Administration is intended only from an approved bastion with fixed private address 10.20.5.10; its route to the instance is already working. Public HTTPS access must remain. An approved recovery console is available.

Describe the smallest inbound-rule change and a safe verification sequence. Include an allowed administration test, a prohibited-source test and an HTTPS regression test. Explain why replacing both existing rules with one blanket deny would not meet the requirements.

### T7 — Evaluate a recovery result (3.1, 3.3)

A service has an RPO of 15 minutes and an RTO of 60 minutes. At the simulated 10:00 outage, the newest usable recovery point contains data through 09:30. The complete service, including dependencies, is restored at 10:45. The exercise started at 10:00; no additional unmeasured outage interval exists.

Calculate data loss and service outage against the targets. Which target is met? Identify a useful corrective study action and the next test; do not infer that a successful restore proves the backup frequency is adequate.

### T8 — Trace the return path through a stateless boundary (1.3, 4.3, 5.3)

An AWS client at 10.20.1.8 makes a TCP connection from source port 55000 to server 10.20.2.10:443 in a different subnet. The route tables and client-side controls allow both directions. The server security group permits this client on TCP 443. The server subnet's custom network ACL permits inbound TCP 443 from the client subnet, but its only outbound permit is TCP destination port 443 to the client subnet. All other traffic is denied. Flow evidence shows the server's reply to destination port 55000 denied at that subnet boundary.

Which control needs the targeted correction? Specify source/destination direction and destination port for the denied reply. Explain why adding another inbound TCP 443 security-group rule would not solve the observed denial. State a bounded test and how a production port-range decision differs from this single known connection.
