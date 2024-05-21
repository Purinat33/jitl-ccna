# IPv4 Configuration (Cisco Devices)

![[img/DAY 8 - Cisco IPv4 Configuration.png | center]]

* **3** LAN connected through a router **R1**:
	* `10.0.0.0/8` network connected to R1 through the `G0/0` Interface, which is assigned the address `10.255.255.254`
	* `172.16.0.0/16` network connected to R1's `G0/1` Interface, with an IP address of `172.16.255.254`
	* `192.168.0.0/24` network connected to the R1's `G0/2` Interface, the interface is assigned the address `192.168.0.254`

<hr>

## Configuring the R1 Router.

### Pre-Configuration:
* Connecting to the Router's console.

![[img/DAY 8 - Cisco IPv4 Configuration.jpg]]

* Changing the Router's hostname to **R1**

![[img/DAY 8 - Cisco IPv4 Configuration-1.png]]

* View the router's interfaces status with `show ip interface brief`:

![[img/DAY 8 - Cisco IPv4 Configuration-3.png | 600]]

* **Notes**:	
	* **Status**: *Layer 1 (Physical)* Status.
		* `administratively down` = Interface has been **disabled** using the `shutdown` command. 
			* This is the **Default Status** of Cisco *Router* Interfaces.
			* Whereas Cisco *Switch* Interfaces are not `administratively down` by default.
	* **Protocol**: *Layer 2 (Data Link)* Status.
### Configuration:

1. Enter **Sub-Configuration** mode for interface `G0/0`:

![[img/DAY 8 - Cisco IPv4 Configuration-4.png]]

2. Set the wanted IP and mask.

![[img/DAY 8 - Cisco IPv4 Configuration-5.png | 512]]

3. Enable the **G0/0** using `no shutdown`

![[img/DAY 8 - Cisco IPv4 Configuration-6.png]]

4. View **G0/0** Interface's Details using `show interfaces g0/0`. (With an `s`. Try not to be confused with `show ip interface brief` that has none).

![[img/DAY 8 - Cisco IPv4 Configuration-7.png]]

5. Repeat for all the interfaces.

<hr>

# Summary:

1. `R1# show ip address brief`: View information about IP Addresses on each router's interface.
	1. **Administratively Down**: Interface is disabled with a `shutdown` command, a default **Status** for routers.
	2. **Protocol**: Data Link Layer's Status.
2. `R1# show interfaces g0/0`: View information about a *specific* interface.
3. `R1(config)# interface g0/0`: Enter a specific interface configuration (eg. **G0/0**)
4. `R1(config-if)# ip address 192.168.1.1 255.255.255.0` 
	* Will still be disabled until a `no shutdown` on that interface is performed.

<hr>

