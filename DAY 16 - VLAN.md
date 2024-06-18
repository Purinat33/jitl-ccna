# Virtual LAN (VLAN)

## What is a LAN?

* Previously it was stated that a **LAN** is a group of devices (PCs, Servers, Routers, Switches etc.) *in a single location* (home, office, etc.)
* A more specific definition:
	* A **LAN** is a *single* **Broadcast Domain**, including all devices in that broadcast domain. 
		* A **Broadcast Domain** is the group of devices which will receive a *broadcast frame* (**Destination MAC**: `FFFF.FFFF.FFFF`) sent by any one of the members.
		* A router's interface will receive its connected network's broadcast frame but not beyond it. 

![[img/DAY 16 - VLAN.png]]

## LAN Problems:

For example, imagine a workspace with some PCs being divided into three departments.

![[img/DAY 16 - VLAN-1.png]]

However, this isn't considered the best setup because, for example, a Security PC's broadcast for the department will be broadcasted to HR and IT as well. (Not good for performance and security).

It's better to split into three different subnets, one for each department.

![[img/DAY 16 - VLAN-3.png]]

But how will the router knows how to send traffic to each network? Which interface for which subnet? Or we connect 3 interfaces to the 3 subnets?

![[img/DAY 16 - VLAN-4.png]]

So instead of Engineering's PC0 sending messages directly to Sale's PC7 through the Switch sitting clearly in the middle, it will have to send the messages to the Switch, into the Router, and into the Switch and finally to the intended destination. (Very convoluted).

Also the switch will broadcast frames to those different subnets anyway (ARP, Broadcast MAC), since Switch operates on Layer 2 and not Layer 3 it cannot differentiates between each subnet's network address. 

**Although we separated the three departments into three subnets (*Layer 3*), they are still in the same *Broadcast Domain* (*Layer 2*).**

This is how why we use **VLAN** instead of buying more routers and switches.

<hr>

## VLAN:

Assign different **VLAN**s to different departments.

![[img/DAY 16 - VLAN-5.png]]

We configured VLAN in the **Switch** interface. A device connecting to a switch's interface will inherit that interface's VLAN. 

**A switch Will Not forward traffic between VLANs, including *broadcast and unknown unicast* traffics**

Note that **The switch does not perform *inter-VLAN routing*. It must send the traffic through the router (Default Gateway)**.

![[img/DAY 16 - VLAN-6.png]]

<hr>

## VLAN (cont.):

* are configured on *Switches* on a **per-interface** basis.
* **Logically** separate end hosts at Layer 2.
* Switches do not forward traffic directly between hosts in different VLANs.

<hr>

## VLAN Configuration:

![[img/DAY 16 - VLAN-8.png]]

Use command `show vlan brief`
![[img/DAY 16 - VLAN-9.png]]
* VLANs 1 & 1002-1005 exist by default and **Cannot be deleted.**
* All interfaces are in VLAN 1 by default.

### Assigning interfaces to a VLAN

Assigning **VLAN 20** to interfaces *Fa0/15 to Fa0/16*
![[img/DAY 16 - VLAN-10.png]]
1. Accessing a range of interfaces.
2. Set the interfaces as **Access Ports**
	1. An access port is a switchport which belongs to a single VLAN, and usually connects to end hosts like PCs.
	2. Switchports which carry multiple VLANs are called **Trunk Ports**, which will be explained later.
3. Assigns the VLAN to that port.

![[img/DAY 16 - VLAN-13.png]]

### Checking VLANs Config:

![[img/DAY 16 - VLAN-14.png]]

### VLAN Sub-Config Mode:

* With `vlan <vlan>` command:

![[img/DAY 16 - VLAN-15.png]]

![[img/DAY 16 - VLAN-16.png]]

<hr>