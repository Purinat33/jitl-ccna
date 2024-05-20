# IPv4 Addresses

* 32 bits addresses.
* Separated into 4 octets of 8 bits each.
* Written in dotted decimal notation

| 192      | 168      | 1        | 254      |
| -------- | -------- | -------- | -------- |
| 11000000 | 10101000 | 00000001 | 11111110 |
Each octet have values from 0-255.

## Network and Host portion:

eg. `192.168.1.2`**/**`24`

* `/24` bits netmask signifies **How many bits are used to identified the network portion** (Which network the IP belongs to).
	* <u><b>192.168.1</b></u>.0 Network.
	* 192.168.1.<u><b>2</b></u> Host
	* `24` bits are used to identify the Network.
	* 32-`24` = `8` bits are used to identify the Host.

## Netmask

* How many bits are used to identified the network portion.
eg.
* `/8` 
	* 8 bits network portion.
	* `11111111`.00000000.00000000.00000000
	* `255`.0.0.0
* `/16`
	* 16 bits network portion.
	* `11111111`.`11111111`.00000000.00000000
	* `255`.`255`.0.0
* `/24`
	* 24 bits network portion.
	* `11111111`.`11111111`.`11111111`.00000000
	* `255`.`255`.`255`.0
* `/21`
	* 21 bits network portion.
	* `11111111`.`11111111`.`11111000`.00000000
	* `255`.`255`.`248`.0

<hr>

![[img/DAY 6 - IPv4.png]]

* `192.168.1.0/24` Network
	* PC1: `192.168.1.2`
	* PC2: `192.168.1.3`
	* R1's G0/0 Interface: `192.168.1.1`
* `172.69.0.0/16` Network
	* PC3: `172.69.5.7`
	* PC4: `172.69.255.142`
	* R1's G0/1 Interface: `172.69.1.0`

<hr>

## IPv4 Address Classes:

![[img/DAY 6 - IPv4-2.png]]

![[img/DAY 6 - IPv4-1.jpg]]

**What is Loopback Address**:
* Notice Class A nor B have `127.x.x.x`.
* This is because `127.x.x.x` ranges are used for **Loopback Addressing**
* Address used to test the network model on the local device.
  ![[img/DAY 6 - IPv4-1.png]]
  
  <hr>

## Important IP Addresses in each network:

1. **Network Address**: When all host's bits == `0`
2. **Broadcast Address**: When all host's bits == `1`
(These cannot be used as host/device's IP Addresses)
   
eg. `192.168.6.4/24`
* **Network Address** = 192.168.6.`00000000` (192.168.6.*0*)
* **Broadcast Address** = 192.168.6.`11111111` (192.168.6.*255*)
  
3. **First Usable Host Address** = The IP address *after* the network address.
4. **Last Usable Host Address** = The IP address *before* the broadcast address.

eg. `192.168.6.4/24`
* **Network Address** = 192.168.6.`00000000` (192.168.6.*0*)
* **Broadcast Address** = 192.168.6.`11111111` (192.168.6.*255*)
* **First Host** = 192.168.6.1
* **Last Host** = 192.168.6.254
  
5. **Number of usable hosts**: `pow(2, 32-netmask) - 2`

eg. `192.168.6.4/24`
* **Network Address** = 192.168.6.`00000000` (192.168.6.*0*)
* **Broadcast Address** = 192.168.6.`11111111` (192.168.6.*255*)
* **First Host** = 192.168.6.1
* **Last Host** = 192.168.6.254
* **Usable Hosts** = `pow(2 , 32-24) - 2` = 256 - 2 = 254
  
<hr>

# Summary

**IPv4 Address Classification**:
![[img/DAY 6 - IPv4-2.png]]

![[img/DAY 6 - IPv4-1.jpg]]
* `127.x.x.x`: **Loopback Address**, for testing networking on the local device.
 
**IP Address**:
* Separated in 4 Octets of 8 bits each.
* Each octet can have value between `0` to `255`.
* `x.x.x.x/y` with `/y` netmask denoting how many *bits* are part of the *Network* identifier, while the remaining bits identify the unique *host* within that Network.
* **Important IP Address** given an IP:
	* **Network IP**: The identifier of *the Network* itself.
		* All Host bits = `0`
	* **Broadcast IP**: The broadcast address of that network.
		* All Host bits = `1`
		  
	<u>eg:</u> Given a **Class B** IP address of `172.16.59.4/16`:
	1. **Netmask**: `/16`
	2. **Network Portion**: `172.16`.59.4
	3. **Host Portion**: 172.16.`59.4`
	4. <u><b><i>Network Address</i></b></u>: `172.16.0.0`
	5. <u><b><i>Broadcast Address</i></b></u>: `172.16.255.255`
	6. **First Usable Address**: `172.16.0.1`
	7. **Last Usable Host**: `172.16.255.254` 
	   

**Fast identifying important IPs will be in a separate note**

<hr>

