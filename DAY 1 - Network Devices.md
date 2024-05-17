
# Networking Devices

**Networking** allows devices (`nodes`) to communicate.

## Types of Nodes:
### 1. End Host or Endpoint:
1. **Client**: Accesses services from the server.
2. **Server**: Provides services to the client.
![[img/DAY 1 - Network Devices.png | center]]
### 2. Intermediate:
1. **Switch**: Routes traffics **within** the same Local Area Network (the same `LAN`)
	* e.g. Cisco *Catalyst* Series
	![[img/DAY 1 - Network Devices-2.png | center]]
	
2. **Router**: Routes traffics **between** other networks (other LANs)
	* e.g. Cisco *ISR* Series
	![[img/DAY 1 - Network Devices-3.png | center]]
3. **Firewall**: Monitor and filter traffics based on set of rules. Can be placed *outside* or *inside* a LAN
	* e.g. Cisco *ASA* series (**Classic**)
	![[img/DAY 1 - Network Devices-4.png | center]]
	* e.g. Cisco *Firepower* series (**Next-Generation**)
	![[img/DAY 1 - Network Devices-5.png | center]]

	* **Network** vs. **Host-based** Firewall:
		![[img/DAY 1 - Network Devices-6.png]]
		* **Network-Based** are hardware firewalls that filter traffics entering a network.
		* **Host-Based** are software that filters traffics entering or leaving a *host*.
			* **Host-Based Firewalls** are <u><b>outside</b></u> the scope of CCNA.

<hr>

## Packet Tracer Activity

![[img/DAY 1 - Network Devices-7.png]]

