# Static Routing

## Review: `Local` & `Connected` Routes:

![[img/DAY 11 - Routing Fundamental.jpg | center | 600]]

![[img/DAY 12 - Static Routing.png]]

![[img/DAY 12 - Static Routing-1.png | center | 600]]

The following routes are automatically added to the routing table for each interface with an IP address configured:
1. **`C` - Connected**:
	1. A route to the network the interface is connected to. (With the actual netmask configured on the interface).
2. **`L` - Local**:
	1. A route to the actual IP address configured on the interface. (With a `/32` netmask)
R2 knows how to reach its own IP addresses and destinations in its connected networks, **but** it doesn't know how to reach destinations in remote networks.
* **Knows**:
	* `192.168.12.0/24` (including `192.168.12.2/32`)
	* `192.168.24.0/24` (including `192.168.24.2/32`)
* **Doesn't know**:
	* `192.168.1.0/24`
	* `192.168.13.0/24`
	* `192.168.34.0/24`
	* `192.168.4.0/24`

<hr>

## Default Gateway

![[img/DAY 12 - Static Routing-3.png]]
* End hosts like **PC1** and **PC4** can send packets directly to destinations *within* their connected network.
	* **PC1** is connected to `192.168.1.0/24`
	* **PC4** is connected to `192.168.4.0/24`
* To send packets to destinations *outside* their local network, they must send the packets to their **Default Gateway**.
	* Configuring interfaces on a Linux PC:
		* **PC1** Linux Config:
			![[img/DAY 12 - Static Routing-4.png | center | 512]]
		* **PC4** Linux Config:
			![[img/DAY 12 - Static Routing-5.png | center | 512]]
* The **Default Gateway** configuration is also called a **Default Route**:
	* It is a route to `0.0.0.0/0` = all netmask bits set to `0`.
		* Includes all addresses from `0.0.0.0` to `255.255.255.255`
		* The **Default Route** is the ***LEAST*** specific route possible, because it includes ***All*** the IP addresses.
			* `0.0.0.0/0` = 4,294,967,296 IP addresses.
		* The **Local Route** is the ***MOST*** specific route possible, because it includes ***One*** IP address.
			* `192.168.1.1/32` = 1 IP address.
* End hosts usually have no need for any more specific routes.
	* They just need to know that *"To send packets outside my local network, I should send them to my **default gateway**."*
		* **Source IP**: `192.168.1.10`
		* **DST IP**: `192.168.4.10`
		* ***DST MAC***: R1's **G0/0** MAC
			* To learn R1's **G0/0** MAC address, PC1 will first send an **ARP Request** to `192.168.1.1`
		* **SRC MAC**: PC1's **eth0** MAC

![[img/DAY 12 - Static Routing-3.png | center | 600]]

* When R1 receives the frame from PC1, it will de-encapsulate it (remove L2 header/trailer) and look at the inside packet.
* It will check its routing table for the most specific matching route:
	![[img/DAY 11 - Routing Fundamental-4.png| center | 650]]
* R1 has no matching routes in its routing table.
	* It will drop the packet.
* To properly forward the packet, R1 needs a route to the destination network of `192.168.4.0/24`.
	* Routes are instructions: *"To send a packet to destinations in network **`192.168.4.0/24`**, forward the packet to **`Next Hop Y`**"*
* There are two possible path packets from **PC1 to PC4** can take:
	1. PC1 → R1 → **R3** → R4 → PC4
	2. PC1 → R1 → **R2** → R4 → PC4
	* For now, we will use the path via **R3** and not **R2**
		* Though it is possible to configure the routers to:
			* **Load-Balance** between path `1` and path `2`.
			* Use path `1` as the main path and path `2` as a backup path.

<hr>

## Static Route Configuration

![[img/DAY 12 - Static Routing-3.png | center | 600]]

* Each router in the path needs ***TWO*** routes:
	* a route to `192.168.1.0/24` (**PC1** network) and
	* a route to `192.168.4.0/24` (**PC4** network)
* This ensures **Two-Way Reachability** 
	* **PC1** can send packets to **PC4** & Vice-Versa.
* Routers don't need routes to all networks in the path to the destination.
	* **R1** doesn't need a route to `192.168.34.0/24`, it only needs to know a route to **R3**. **R3** will handle the route to `192.168.34.0/24` by itself.
	* **R4** also doesn't need a route to `192.168.13.0/24`, **R3** will handle it.
* **R1** already has a **Connected Route** to `192.168.1.0/24`.
* **R4** already has a **Connected Route** to `192.168.4.0/24`
* The other routes (Non-**Connected Routes**) still needed to be manually configured using **Static Route**.
<br><br>
![[img/DAY 12 - Static Routing-3.png | center | 600]]

| Router |   Destination    |    Next-Hop    |   Note    |
| :----: | :--------------: | :------------: | :-------: |
| **R1** | `192.168.1.0/24` | **Connected**  |     -     |
|        | `192.168.4.0/24` | `192.168.13.3` | R3's G0/0 |
|        |                  |                |           |
| **R3** | `192.168.1.0/24` | `192.168.13.1` | R1's G0/2 |
|        | `192.168.4.0/24` | `192.168.34.4` | R4's G0/1 |
|        |                  |                |           |
| **R4** | `192.168.1.0/24` | `192.168.34.3` | R3's G0/1 |
|        | `192.168.4.0/24` | **Connected**  |     -     |
* To allow **PC1 and PC4** to communicate with each other over the network, we will configure the **Static Routes** on **R1, R3, R4** based on the pre-planning table above.
* Use  **`ip route`**`ip-address netmask next-hop`
	* Where:
		* `ip-address`: The **Destination**'s IP address.
		* `netmask`: The netmask of Destination's network.
		* `next-hop`: Next-Hop IP Address
### Demo:

![[img/DAY 12 - Static Routing-7.png | center | 700]]

* Added R1's **Static Route** via: 
	`ip route 192.168.4.0 255.255.255.0 192.168.13.3`
	* Where:
		* `192.168.4.0` = Destination Network
		* `255.255.255.0` = Destination Netmask
		* `192.168.13.3` = Next Hop
* A Code **`S`** **Static Route** is added.
	* The **[1/0]** display for **Static Routes** means:
		* **[Administrative Distance / Metric]**
		* The concept will be covered later.

![[img/DAY 12 - Static Routing-8.png]]
* R3 needed 2 routes.

![[img/DAY 12 - Static Routing-10.png]]
* R4 needed 1 route.

<hr>

## Testing Communication

If the ping is successful, it means that there is two-way reachability.
PC1 can reach PC4 and vice-versa.
![[img/DAY 12 - Static Routing.jpg]]

Note the relationship between IP and MAC address. (**ARP**ing for the **MAC** of the next hop while the IP address stay the same until the end).

<hr>

## `exit-interface`

Instead of configuring next hop, we can configure an exit interface (just send a packet out of this) instead of explicitly telling the ip address of the next hop.

* **`ip route`** `ip-address netmask` *`exit-interface`*
* **`ip route`** `ip-address netmask` *`exit-interface`* `next-hop` 

![[img/DAY 12 - Static Routing-11.png]]
**Note**: Specifying only the `exit-interface` without a `next-hop` will show the Static Route as directly connected.

It is better to specify `next-hop` instead of only having `exit-interface` and without specifying a `next-hop`.

<hr>

## Default Route

* A **Default Route** is a route to `0.0.0.0/0`
	* `0.0.0.0/0 is the *least specific* route possible; it includes every possible IP address.
* If the router doesn't have any more specific routes that match a packet's destination IP address, the router will forward the packet using the **Default Route**.
* A default route is often used to direct traffic to the internet.
	* More specific routes are used for destinations in the internal corporate network.
	* Traffic to destinations outside of the internal network is sent to the internet.
	  ![[img/DAY 11.5 - Static Routing.png]]
	  ![[img/DAY 11.5 - Static Routing-1.png]]
* Gateway of last resort usually means the default route.
* Same structure of command as other `ip route` settings.

<hr>

![[img/DAY 11.5 - Static Routing-2.png]]

<hr>

# Packet Tracer Lab

## Configuration

![[img/DAY 11.5 - Static Routing-3.png]]

## Troubleshooting

![[img/DAY 11.5 - Static Routing-4.png]]

<hr>
