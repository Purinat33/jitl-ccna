# Routing Fundamental

## What is Routing
1. Routing is the process that routers use to determine the path that IP packets should take over a network to reach their destination.
	1. Routers store routes to all of their known destinations in a **Routing Table**.
	2. When routers receive packets, they look in their **Routing Table** to find the best route to forward that packet.
2. There are *two* main routing methods (methods that routers use to learn routes):
	1. **Dynamic Routing**: Routers use Dynamic Routing Protocols (eg. `OSPF`) to share routing information with each other automatically and build their routing tables.
	2. **Static Routing**: A network engineer/admin manually configures routes on the router.
3. A route tells the router: _To send a packet to **`Destination X`**, it should send the packet to ***`Next Hop Y`***_.
	1. Or, if the destination is directly connected to the router, send the packet directly to the **Destination**.
	2. Or, if the destination is the router's own IP address, then **Receive the Packet for Yourself** (and don't forward).

<hr>

## Example Topology:

![[img/DAY 11 - Routing Fundamental.jpg]]

### Pre-routing setup: 
* Example:
	* `R1> en`
	* `R1# conf t`
	* `R1(config)# interface g0/0`
	* `R1(config-if)# ip address 192.168.1.1 255.255.255.0`
	* `R1(config-if)# no shutdown` 
* Repeat for all PC, Routers & Interfaces.
	* **R1**: 
		![[img/DAY 11 - Routing Fundamental.png | center | 512]]
	* **R2**: 
		![[img/DAY 11 - Routing Fundamental-1.png| center | 512]]
	* **R3**: 
		![[img/DAY 11 - Routing Fundamental-2.png| center | 512]]
	* **R4**: 
		![[img/DAY 11 - Routing Fundamental-3.png| center | 512]]

<hr>

### View Routing Table using `show ip route`:

![[img/DAY 11 - Routing Fundamental-4.png| center]]

