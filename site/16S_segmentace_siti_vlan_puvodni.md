# 16. Segmentace sítí - Vlan

## VLAN trunking protocol
VLAN Trunking Protocol allows you to create/delete and modify existing VLANs. This information can then be propagated to other switches that use the same VTP domain. When VTP is first configured it defaults to server mode. VTP information is sent via a trunk port. Uses revision numbers to determine whether the switch needs to update its VTP information.

A few requirements:

Cannot be used on non-Cisco switches
VTP domain must be the same
One switch must be configured in server mode
If a VTP password is used, must be configured on all switches
Three VTP modes:

Server
Can create, add and modify VTP information to other switches.

Transparent
Can create, add and modify VLANs but this isn’t advertised to other switches in the VTP domain, instead these are only local to that switch but a transparent switch will forward VTP advertisements out of trunk ports.

Client
Client mode only receives and forwards VTP updates. Can not create, delete or modify existing VLANs

## Spanning tree protocol 
Spanning Tree Protocol prevents switching loops at layer 2. It elects a root bridge and a root port and does this by sending out BPDUs (bridge protocol data units), a blocked port will still receive BPDUs and needs to receive them in case it needs to come out of the blocked state (link failure, bandwidth changes).

## Rapid Spanning tree protocol
Rapid spanning-tree protocol 802.1w. Faster convergence than spanning-tree protocol hence the ‘rapid’.

RSTP can detect a link failure in 6 seconds (3 hello timers, 2 seconds each)

## Per VLAN Spanning Tree
Default for catalyst switches. Cisco proprietary protocol, allows for creation of per VLAN spanning tree.

## Rapid PVST+
Rapid PVST+ is the IEEE 802.1w (RSTP) standard implemented per VLAN. A single instance of STP runs on each configured VLAN (if you do not manually disable STP). Each Rapid PVST+ instance on a VLAN has a single root switch. You can enable and disable STP on a per-VLAN basis when you are running Rapid PVST+.

