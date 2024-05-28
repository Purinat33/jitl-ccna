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
	* They just need to know that *"To send packets outside my local network, I should send them to my default gateway."*

### IP and MAC relationship
