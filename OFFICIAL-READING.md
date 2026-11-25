# Primary Reading Map: Network+ N10-009

Use these provider-owned pages and standards as starting points. The objective numbers refer to N10-009, not an older exam. The topic descriptions below are original reading prompts; no third-party documents or full-text captures are included. Follow the source attached to a practice question when a more specific product boundary matters.

## Exam scope and complete objective checklist

C1 — CompTIA's Network+ page: https://www.comptia.org/en-us/certifications/network/

C2 — CompTIA's N10-009 objectives, document version 4.0: https://comptiacdn.azureedge.net/webcontent/docs/default-source/exam-objectives/comptia-network-n10-009-exam-objectives-%284-0%29-%281%29.pdf

Start with the provider's current exam page before booking. Read the objectives for all five domains: concepts (1.1–1.8), implementation (2.1–2.4), operations (3.1–3.5), security (4.1–4.3) and troubleshooting (5.1–5.5). The study guide gives a prompt for every objective; this short technical reading map is selective, not a complete textbook or substitute for those objectives.

## Addressing, routing and network services

R1 — Microsoft TCP/IP addressing and subnetting: https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/tcpip-addressing-and-subnetting

Read the subnet-mask and subnetting examples. Use them to justify network boundaries and valid host ranges, not just to memorize mask values. Objectives 1.7, 2.1, 5.3; exercises S1–S6.

R2 — RFC 4632, CIDR: https://www.rfc-editor.org/rfc/rfc4632

Read section 3.1 for address blocks and prefix-length notation. Relate prefix size to allocation and routing. Objectives 1.7, 2.1; S1–S6.

R3 — RFC 1918, private IPv4 addresses: https://www.rfc-editor.org/rfc/rfc1918

Read section 3 for the private ranges. Private address space does not by itself supply encryption, reachability or a safe security policy. Objectives 1.7, 4.1.

R4 — RFC 3927, IPv4 link-local: https://www.rfc-editor.org/rfc/rfc3927

Read the introduction and section 2 for scope and behavior. An observed link-local address calls for investigating expected address assignment; it does not establish a failed router. Objectives 1.7, 3.4, 5.3; T1.

R5 — RFC 2131, DHCP: https://www.rfc-editor.org/rfc/rfc2131

Read section 3.1 for address allocation and the exchange involving clients, servers and relay behavior. Relate scope availability and path evidence to a client that lacks a lease. Objectives 3.4, 5.3; T1.

R6 — RFC 1034, DNS: https://www.rfc-editor.org/rfc/rfc1034

Read sections 4 and 5 for name-server and resolver roles. Distinguish an authoritative answer, a cached answer and an application connection. Objectives 1.4, 3.4, 5.3; T2.

R7 — RFC 8200, IPv6: https://www.rfc-editor.org/rfc/rfc8200

Read sections 3 and 4 for header and extension-header structure. Pair this with the objectives' IPv6 and transition topics; the protocol specification is not a platform configuration recipe. Objectives 1.8, 3.4.

## Endpoint tools: ask a specific question

R8 — Microsoft ipconfig: https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig

Use the `/all` documentation to interpret adapter configuration and DHCP status. Read renewal/release behavior before touching an active adapter; do not release a remote management connection casually. Objectives 3.4, 5.3, 5.5; T1.

R9 — Microsoft nslookup: https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/nslookup

Read the syntax for specifying a DNS server and a query. A successful query to a chosen server does not prove the client uses that server for all lookups. Objectives 3.4, 5.3, 5.5; T2.

R10 — Microsoft ping: https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ping

Read what an echo request/reply tests. An absent reply may reflect filtering; a successful reply does not prove that an application port is available. Objectives 5.1, 5.5.

## Switching, cabling and wireless interpretation

R11 — Cisco, Troubleshoot Switch Port and Interface Problems: https://www.cisco.com/c/en/us/support/docs/switches/catalyst-6500-series-switches/12027-53.html

Read the VLAN/trunking, physical connection and interface-counter discussions. Translate the troubleshooting reasoning to your equipment; commands and supported features vary by platform and software. Objectives 2.2, 5.2, 5.3, 5.5; T3, T4.

R12 — Cisco, Wireless RF Reference Guide: https://www.cisco.com/c/en/us/td/docs/wireless/controller/9800/technical-reference/wireless-rf-reference-guide.html

Read the RF, channel-width and interference discussions. Separate signal level from airtime competition, and follow local regulatory constraints. Objectives 2.3, 5.4; T5.

## Security boundaries, cloud operations and recovery

R13 — AWS VPC security groups: https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html

R14 — AWS VPC network ACLs: https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html

Compare resource-level stateful security groups with subnet-level stateless network ACLs. These are an AWS example, not a claim that every firewall behaves the same way. Inspect routing as well as policy when tracing a connection. Objectives 1.3, 4.1, 4.3, 5.3; T6, T8.

R15 — AWS, What Is Disaster Recovery?: https://aws.amazon.com/what-is/disaster-recovery/

Read the RPO and RTO definitions and relate them to measured restoration and data-loss results. The definitions are useful beyond AWS; an actual recovery design still requires dependency and restore testing. Objectives 3.1, 3.3; T7.

## Using a reference well

Write down the section and the decision it changes. For an old platform-specific manual, use the linked behavior to understand the example and then consult the current manual for your actual device. Recheck the provider's exam objectives and current product documentation before making a real operational change. Links are for reading at the publisher; this companion does not grant redistribution rights to those works.
