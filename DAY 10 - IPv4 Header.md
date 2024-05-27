# IPv4 Header

![[img/DAY 10 - IPv4 Header.jpeg]]
Read the image from: *left to right* then *top to bottom*
<hr>

## Components in the IPv4 Header:

1. **Version** (4 bits): Identifies the version of IP being used.
	1. `0100` = IPv4
	2. `0110` = IPv6
2. **IHL (Internet Header Length)** (4 bits): 
	1. Indicate the total length of the header using **4-Bytes Increment** 
		1. eg. **IHL** = 5 multiply by `4 Bytes Increment` = 20 Bytes.
	2. Minimum value of **IHL** = 5. (x4 = 20 bytes).
	3. Maximum value of **IHL** = 15. (x4 = 60 bytes).
	![[img/DAY 10 - IPv4 Header.png]]
	 4. The size depends on the **Options** field:
		 1. Size 0 **Options** + Minimum **IHL** size (20) = 20+0 Bytes.
		 2. Size 40 **Options** + Minimum **IHL** = 20 + 40 = 60 Bytes.
	5. IPv4 Header size = 20 - 60 Bytes.
3. **DSCP (Differentiated Services Code Point)** (6 bits):
	1. **DSCP** is used for **QoS (Quality of Service)**
	2. Used to prioritize delay-sensitive data (eg. *streaming voices, videos etc.*)
4. **ECN (Explicit Congestion Notification)** (2 bits):
	1. Provides End-to-End (between two endpoints) notification of network congestion **without dropping packets**. (Normally congestion = Packet Dropped)
	2. Optional feature that requires both endpoints, as well as the underlying network infrastructure, to support it.
	3. The chart combines **DSC + ECN** into **TOS (Type of Service)**.
5. **Total Length** (16 bits):
	1. Indicates the total length of the **packet** (not just the header).
	2. Measured in *Bytes* (Not **4-Bytes Increment** like in **IHL**)
	3. Minimum Value = **20** (IPv4 Header with no encapsulated data).
	4. Maximum Value = **65,535** (All `1` in 16-bits).
6. **Identification** (16 bits):
	1. If a packet is fragmented due to being too large, this field is used to identify **which packet the fragment belongs**.
	2. All fragments of the *same packet* will have their own IPv4 header with the *same value* in this field.
	3. Packets are fragmented if larger than the **MTU (Maximum Transmission Unit)**.
7. **Flags** (3 bits):
	1. Used to control/identify fragments.
	2. **Bit 0**<sup>th</sup>: `Reserved`, always set to `0`
	3. **Bit 1**<sup>st</sup>: `Don't Fragment` (**DF**), used to indicate a packet that should not be fragmented.
	4. **Bit 2**<sup>nd</sup>: `More Fragment` (MF)
		1. Set to `1` if there are more fragment in the packet.
		2. Set to `0` for the last fragment.
		3. Unfragmented packets will always have MF bit = 0)
8. **Fragment Offset** (13 bits):
	1. Used to indicate the position of the fragment within the original, unfragmented IP Packet.
	2. Allows fragmented packets to be reassembled by the receiving host even if the fragments arrive out of order.
9. **TTL (Time To Live)** (8 bits):
	1. A router will drop a packet with TTL = 0
	2. Used to prevent infinite loops.
	3. Originally designed to indicate the packet's maximum lifetime in seconds.
	4. In practice, indicates a **Hop Count**:
		1. Each time the packet arrives at a router, decrement the TTL by 1.
	5. Recommend value = 64
10. **Protocol** (8 bits):
	1. Indicates the protocol of the encapsulated **Layer 4 PDU**
		1. Value of `6`: **TCP**
		2. Value of `17`: **UDP**
		3. Value of `1`: **ICMP** (Ping)
		4. Value of `89`: **OSPF** (Dynamic Routing Protocol)
11. **Header Checksum** (16 bits):
	1. A calculated checksum used to check for errors in the IPv4 Header.
	2. When a router receives a packet, it calculates the checksum of the header and compares it to the value in this field of the header.
	3. If they do not match, the router drops the packet.
	4. Used to check for errors **ONLY** in the IPv4 Header.
	5. IP relies on the encapsulated protocol to detect errors in the encapsulated data/payload.
12. **Source IP Address** (32 bits)
	1. IPv4 address of the sender of the packet.
13. **Destination IP Address** (32 bits)
	1. IPv4 address of the intended receiver of the packet.
14. **Options** (0-320 bits):
	1. Rarely used.
	2. If the **IHL** field is greater than 5, it means that **Options** are present.
	3. **Not Required for CCNA**

## Wireshark Example:
![[img/DAY 10 - IPv4 Header-1.png]]

![[img/DAY 10 - IPv4 Header-2.png]]

<hr>

