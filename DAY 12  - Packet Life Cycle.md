# The Life of a Packet

This is already covered in previous days, but this is more of a summary into one big picture.

## Network Topology

![[img/DAY 12  - Packet Life Cycle.png | center | 600]]
* Looking at the packets going from `192.168.1.10/24` to `192.168.4.10/24` 
* All **Static Routes** have been configured to allowed `192.168.1.0/24` network to communication with `192.168.4.0/24` 
* We're gonna use some **MAC Addresses** as well in addition to existing **IP**s.

| Device        | PC1  | R1   | R1   | R2   | R2   | R4   | R4   | PC4  |
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| **Interface** | -    | G0/0 | G0/1 | G0/0 | G0/1 | G0/0 | G0/2 | -    |
| **MAC**       | 1111 | aaaa | bbbb | cccc | dddd | eeee | fffe | 4444 |

## Life Cycle

![[img/DAY 12  - Packet Life Cycle-1.png | center | 600]]
### To R1:
1. **PC1** creates a packet with this IP header to **PC4**:
	1. **SRC**: `192.168.1`.10
	2. **DST**: `192.168.4`.10
2. **PC1** sees that the **Destination** is in a different network.
	1. It sends the packet to its **Default Gateway** (**R1**)
3. **PC1** does not know the **MAC Address** of **R1**.
	1. It will use **ARP** (**Address Resolution Protocol**)
4. **PC1** creates an **ARP Request Packet**:
	1. **SRC IP**: `192.168.1.10`
	2. **DST IP**: `192.168.1.1`
	3. **DST MAC**: *`FFFF.FFFF.FFFF`* (**Broadcast MAC**)
	4. **SRC MAC**: `xxxx.xxxx.1111` (Kept last 4 digits for simplicity)
5. **SW1** floods the frame on all port except the source port. (To R1's G0/0)
6. **R1's g0/0** matches the request frame with its own IP, and creates an **ARP Reply**:
	1. **SRC IP**: `192.168.1.1`
	2. **DST IP**: `192.168.1.10`
	3. **DST MAC**: *`1111`* (**Unicast MAC**)
	4. **SRC MAC**: `aaaa` 
7. **PC1** now *encapsulate* the original packet with the Ethernet header to **R1's**:
	1. **IPv4** Header:
		1. **SRC**: `192.168.1`.10 (**PC1**)
		2. **DST**: `192.168.4`.10 (**PC4**)
	2. **Ethernet** Header:
		1. **DST**: `aaaa` (**PC1**) 
		2. **SRC**: `1111` (**R1's g0/0**)

### From R1 to R2:

![[img/DAY 12  - Packet Life Cycle-3.png]]

1. **R1** receives the frame from PC1 and *remove* the **Ethernet Header** (The *IPv4 Header* stays the same).
2. **R1** looks up its routing table for `192.168.4.10`:
	1. The most specific match is for **Destination: `192.168.4.0/24`** with the **Next Hop: `192.168.12.2`**:
		![[img/DAY 12  - Packet Life Cycle-4.png | center | 600]]
3. **R1** will now encapsulate the packet with the ethernet header for `192.168.12.2`'s **MAC Address**:
	1. **R1** performs **ARP** for **R2's** MAC Address.
		1. **SRC IP**: `192.168.12.1` (R1's g0/1)
		2. **DST IP**: `192.168.12.2` (R2's g0/0)
		3. **DST MAC**: *`FFFF.FFFF.FFFF`*
		4. **SRC MAC**: `bbbb`
4. **R2's g0/0** receives the **ARP Request**, it replies with its own **MAC Address** to **R1's g0/1**:
	1. **SRC IP**: `192.168.12.1` (R1's g0/1)
	2. **DST IP**: `192.168.12.2` (R2's g0/0)
	3. **DST MAC**: `bbbb`
	4. **SRC MAC**: `cccc`
5. **R1** encapsulates the still-the-same IPv4 header with the new Ethernet Header, with **R2's g0/0** MAC Address being the destination MAC Address.

The same pattern is used for **R2 to R4** and **R4 to PC4** with the **ARP Request/Reply** for the MAC address of the next hop, **De-Encapsulation** of the Ethernet Header at each hop while the IPv4 Packet stays the same the entire time.

<hr>

# LAB:

![[img/DAY 12  - Packet Life Cycle-5.png]]
