# Worked Answers and Evidence Guide

Compare your reasoning before checking your final value. Reference IDs resolve to `OFFICIAL-READING.md`. These are paper solutions to fictional scenarios, not claims of live lab execution. More than one diagnostic command can be appropriate if it tests the stated boundary safely.

## Subnetting answers

### S1 — Containing /26 block

The mask is 255.255.255.192. A /26 has 64 addresses and 62 usable LAN host addresses. The host lies in 192.0.2.128/26: network .128, broadcast .191, usable .129–.190. Gateway .129 is an on-subnet usable address. Address .192 begins the next /26, so it is neither in this subnet nor a usable host of that next block. References: R1, R2.

### S2 — Equal-size /27s

Use /27, mask 255.255.255.224. Its 32 addresses give 30 usable hosts; /28 offers only 14 and fails the requirement. Borrowing three bits from /24 gives eight /27 subnets. Their starts advance by 32: .0, .32, .64, .96 and so on. The third is 198.51.100.64/27, usable .65–.94, broadcast .95. Six subnets can be assigned and two retained. References: R1, R2.

### S3 — Largest-first VLSM

The allocation is 10.44.8.0/25 for 100: usable .1–.126, broadcast .127, capacity 126. Next is 10.44.8.128/26 for 50: usable .129–.190, broadcast .191, capacity 62. Next is 10.44.8.192/27 for 20: usable .193–.222, broadcast .223, capacity 30. Last is 10.44.8.224/28 for 10: usable .225–.238, broadcast .239, capacity 14.

The remaining block is 10.44.8.240/28, covering .240–.255. The allocated block sizes total 128 + 64 + 32 + 16 = 240 addresses. Each start is correctly aligned and no ranges overlap. Assigning a /27 to the 50-host LAN would fail even though the entire /24 has spare capacity. References: R1, R2.

### S4 — Broadcast is not a spare host

The block covers 203.0.113.64–203.0.113.79. Address .64 is the network, .79 is the broadcast and .65–.78 are usable. Choose .78 from the supplied candidates, reserve it in the address plan and confirm the actual mask and gateway at installation. An unassigned address can still be reserved by subnet semantics; duplicate checks alone cannot make a broadcast address usable. References: R1, R2.

### S5 — The /23 spans two /24s

Mask 255.255.254.0 produces network 172.20.10.0/23, broadcast 172.20.11.255, usable 172.20.10.1–172.20.11.254 and 510 usable LAN addresses. The block advances in steps of two in the third octet. Address 172.20.10.55 is on-link; 172.20.12.10 is outside. Under the stated routing assumptions, the host sends the off-link packet via its default gateway, resolving the gateway's local link-layer address rather than trying to find the remote destination directly on the LAN. References: R1, R2.

### S6 — Correct the block, not just the gateway

Engineering covers 192.168.40.0–.127. The proposed Voice block covers .64–.127, so that entire /26 overlaps Engineering. The lowest available aligned replacement is 192.168.40.128/26: usable .129–.190, broadcast .191. Addresses .192–.255 remain outside both allocations. A gateway change within the old Voice prefix leaves the overlap intact; revise the subnet allocation and dependent addressing through a documented change. References: R1, R2; objective 3.1 for address-plan maintenance.

## Troubleshooting answers

### T1 — Investigate the expected DHCP path

The link-local address and missing gateway are consistent with the workstation not obtaining its intended routable DHCP configuration. They do not prove that the central server is down. A working lease on VLAN 20 demonstrates service for that path, not the VLAN 30 relay path.

Inspect VLAN 30 relay configuration and authorized client/relay/server logs or a permitted capture: does a client discovery reach the relay and server, does an offer return, and does the request/acknowledgment complete? Compare relay interface/subnet information and the actual return path. This distinguishes a missing or misdirected relay, a filtered exchange and a server response issue without assuming one cause. After the approved repair, validate a VLAN 30 address, mask, gateway and lease, then the required service path. Do not install a random static address as evidence that DHCP is restored. References: R4, R5, R8.

### T2 — Compare the resolver's answer and cache state

Investigate resolution through 192.0.2.53 first. Compare the queried record type, the authoritative value, the resolver's cached value and TTL, and whether the resolver follows the intended zone/forwarding path. A recent update can legitimately coexist with an older unexpired cached answer. Check the approved record and TTL behavior before clearing a shared cache or editing DNS.

The direct TCP test already establishes this client's path to that address and port for this test. Restarting the application does not explain the inconsistent name answers. Clearing only the client's cache will not fix a shared resolver that still returns the old data. Verify the expected answer through the client's normal resolver path after the appropriate expiry or authorized correction, then connect to the service by name on TCP 8443. An nslookup success alone is not application validation. References: R6, R9, R10.

### T3 — Carry VLAN 30 on the trunk

The shared link excludes VLAN 30 even though the VLAN and access memberships exist. Under change approval, add VLAN 30 to the permitted list at both ends while retaining VLANs 10 and 20; do not replace the list with only 30. Save the initial configuration so rollback restores the original permitted list if the change causes harm.

Check the operational trunk/VLAN state, then test cross-switch VLAN 30 communication and existing VLAN 10/20 traffic. Verify other applicable controls rather than promising that any single command is sufficient on every switch. Same-subnet communication across the switched path does not require a new host default gateway. References: R11; objectives 2.2, 5.3.

### T4 — Narrow the suspect physical segment

The controlled comparison supports a fault associated with the removed patch lead or its previous connection/contact. It does not by itself prove which conductor failed, exclude a reseating effect or establish long-term stability. Preserve the suspect lead for permitted cable testing instead of returning it to service unexamined.

Continue the comparable workload for a suitable observation window, compare error-counter deltas rather than old cumulative totals, and verify service performance and stability. Record the original symptoms, lead change, unchanged controls, counter observations and outcome. Moving the port and changing duplex simultaneously would introduce multiple changed variables and prevent attributing the improvement to this physical segment. References: R11; objectives 5.1, 5.2, 5.5.

### T5 — Pilot an airtime improvement

Use an approved limited pilot to steer suitable clients to the surveyed 5 GHz channel/band, keeping a known rollback configuration. Compare channel utilization, retries, latency, loss and actual call quality under a comparable meeting load, plus coverage and roaming for the affected clients. Roll back or revise the pilot if coverage, compatibility or service quality regresses.

High signal already exists; more power everywhere does not create more airtime and can enlarge contention domains or worsen interference. The wired control narrows the investigation toward the wireless path for these observations, not toward a universal claim that the upstream network can never fail. Confirm sustained improvement rather than closing on one speed result. References: R12; objectives 2.3, 5.4.

### T6 — Narrow SSH, preserve HTTPS

Replace only the inbound TCP 22 source 0.0.0.0/0 with the approved bastion address 10.20.5.10/32. Retain the public TCP 443 rule. Review all associated security groups for any other SSH allowance because their permissions combine; changing one permissive rule does not override another allowance. Keep the approved recovery console ready before changing management reachability.

Start a new authorized SSH connection from the bastion, test a new connection from a controlled nonapproved source and confirm rejection, and test HTTPS from the intended public path. Existing tracked sessions can outlive a rule change, so do not rely on one old SSH session to prove the new policy. A blanket traffic block would violate required HTTPS and administrative access; AWS security groups use allow rules rather than explicit deny rules. References: R13; objectives 3.5, 4.1, 4.3.

### T7 — Restore time passes, data loss fails

Data loss is 30 minutes, from 09:30 to 10:00, exceeding the 15-minute RPO by 15 minutes. Service outage is 45 minutes, from 10:00 to 10:45, within the 60-minute RTO. Meeting one target does not compensate for missing the other.

Investigate recovery-point creation and usability, such as more frequent tested backups or suitable replication, against the data-loss target. Then repeat a timed end-to-end recovery with measured data currency and dependency restoration. A nominal backup schedule is not enough if the newest backups cannot be used. References: R15; objectives 3.1, 3.3.

### T8 — Permit the known return destination at the ACL

The denied reply is from 10.20.2.10 source TCP port 443 to 10.20.1.8 destination TCP port 55000. The server subnet's outbound network ACL needs an appropriately ordered permit for that reply destination, with the narrow authorized destination address/port scope in this test. Its existing outbound destination-port-443 rule describes the wrong direction of a new client request, not this return packet. Check rule ordering so an earlier deny does not defeat the permit.

Security groups track allowed connections, whereas network ACLs are stateless; both directions must satisfy the ACLs. Another inbound security-group rule cannot override the measured outbound ACL denial. Retry the known connection and confirm the full handshake, service response and relevant flow evidence; retain negative tests for unrelated traffic. In production, derive the necessary client ephemeral-port range and address scope from actual supported clients and policy rather than permanently authorizing only this one observed ephemeral port or opening all traffic. References: R13, R14; objectives 1.3, 4.3, 5.3.
