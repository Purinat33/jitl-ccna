# Routing Fundamental

## What is Routing
1. Routing is the process that routers use to determine the path that IP packets should take over a network to reach their destination.
	1. Routers store routes to all of their known destinations in a **Routing Table**.
	2. When routers receive packets, they look in their **Routing Table** to find the best route to forward that packet.
2. There are *two* main routing methods (methods that routers use to learn routes):
	1. **Dynamic Routing**: Routers use Dynamic Routing Protocols (eg. `OSPF`) to share routing information with each other automatically and build their routing tables.
	2. **Static Routing**: A network engineer/admin manually configures routes on the router.
3. A route tells the router: `To send a packet to` **`Destination X`**, `it should send the packet to` ***`Next Hop`*** **`Y`**.
	1. Or, if the destination is directly connected to the router, send the packet directly to the **Destination**.
	2. Or, if the destination is the router's own IP address, then **Receive the Packet for Yourself** (and don't forward).

<hr>

## Example Topology:
