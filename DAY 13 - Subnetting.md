# Subnetting

## Topics:
1. **CIDR** (Classless Inter-Domain Routing)
2. **Subnetting**

<hr>

## IPv4 **Classes**

| Class | First Octet  | First Octet Range | Prefix |
| :---: | :----------: | :---------------: | :----: |
| **A** | **0**xxxxxxx |      0 - 127      |   /8   |
| **B** | **10**xxxxxx |     128 - 191     |  /16   |
| **C** | **110**xxxxx |     192 - 223     |  /24   |
| **D** | **1110**xxxx |     224 - 239     |   -    |
| **E** | **1111**xxxx |     240 - 255     |   -    |
**Remember**: Only **Class A, B, C** IP addresses can be assigned as a device's address.

### Who Assigned IP Classes?

The **IANA** (**Internet Assigned Numbers Authority**) assigns IPv4 addresses/networks to companies based on their size.

For example, a very large company might receive a **Class A** or **Class B** network, while a small company might receive a **Class C** network.

However, this led to *many wasted* IP addresses.

### IP Wasting

![[img/DAY 13 - Subnetting-1.png]]
* `203.0.113.0/24` **Class C** Network:
	* `203.0.113.0` = **Network ID**
	* `203.0.113.255` = **Broadcast IP**
	* `203.0.113.1` = R1
	* `203.0.113.2` = R2
	* 252 out of 256 IP wasted!

To fix IP wasting, **IETF** (**Internet Engineering Task Force**) introduced **CIDR** in 1993 to replace the "classful" addressing system.

<hr>

## CIDR

* With **CIDR**, the requirements of
	* **Class A** = `/8`
	* **Class B** = `/16`
	* **Class C** = `/24`
	* were *removed*.
* This allowed larger networks to be split into smaller networks.
* These smaller networks are called **Subnetworks** or **Subnets**.

### CIDR Example:

From the previous example:
![[img/DAY 13 - Subnetting-1.png]]

* **Originally** (/24):
	* **Address**: `11001011.00000000.01110001`.**`00000000`**
	* **Mask**: `11111111.11111111.11111111`.**`00000000`**
	* Gives 256 - 2 Hosts 
		* 252 IP Wasted
* **Changing/Borrowing 1 bit** (/25):
	* **Address**: `11111111.11111111.11111111`***`.0`***`0000000`
	* **Mask**: `11111111.11111111.11111111`***`.1`***`0000000` (128)
	* Gives 128 - 2 Hosts = 126 Hosts
		* 124 IP Wasted (Used 2 for R1 & R2 IP addresses)
* **Changing/Borrowing 2 bits** (/26): 
	* **Address**: `11111111.11111111.11111111`***`.00`***`000000`
	* **Mask**: `11111111.11111111.11111111`***`.11`***`000000` (192)
	* Gives 64 - 2 Hosts
		* 60 IP Wasted
* **Changing/Borrowing 3 bits** (/27): 
	* **Address**: `11111111.11111111.11111111`***`.000`***`00000`
	* **Mask**: `11111111.11111111.11111111`***`.111`***`00000` (224)
	* Gives 32 - 2 Hosts
		* 28 IP Wasted
* **Changing/Borrowing 4 bits** (/28): 
	* **Address**: `11111111.11111111.11111111`***`.0000`***`0000`
	* **Mask**: `11111111.11111111.11111111`***`.1111`***`0000` (240)
	* Gives 16 - 2 Hosts
		* 12 IP Wasted
* **Changing/Borrowing 5 bits** (/29): 
	* **Address**: `11111111.11111111.11111111`***`.00000`***`000`
	* **Mask**: `11111111.11111111.11111111`***`.11111`***`000` (248)
	* Gives 8 - 2 Hosts
		*  4 IP Wasted
* **Changing/Borrowing 6 bits** (/30): 
	* **Address**: `11111111.11111111.11111111`***`.000000`***`00`
	* **Mask**: `11111111.11111111.11111111`***`.111111`***`00` (252)
	* Gives 4 - 2 Hosts = 2 Usable addresses.
		*  0 IP Wasted (Both are used for R1 and R2)
		
![[img/DAY 13 - Subnetting-2.png]]

### CIDR: /31 Mask

* **Address**: `11111111.11111111.11111111`***`.0000000`***`0`
* **Mask**: `11111111.11111111.11111111`***`.1111111`***`0` (254) 
* Gives 2 - 2 Hosts = 0 Usable addresses *but*.
	* Why use this?
	* **For *Point-to-Point* Connection** 
		* Normally we'd need 2 for network address and broadcast address.
		* But for **Point-to-Point** communication, there isn't a need for network address or broadcast address. 
		* e.g. 2 routers connection
* ![[img/DAY 13 - Subnetting-3.png]]


### CIDR /32 Mask

* **Address**: `11111111.11111111.11111111`***`.00000000`***
* **Mask**: `11111111.11111111.11111111`***`.11111111`*** (255) 
* Gives 1 - 2 = -1 Usable Hosts???
	* Why use this?
	* For **Static Route** and some other uses.

## CIDR Notation Conversion
![[img/DAY 13 - Subnetting-4.png]]

<hr>

## Subnetting Problems:


![[img/DAY 13 - Subnetting-5.png]]

Divide the `192.168.1.0/24` network into four subnets.

### My Attempt:

* **Original** (/24): 
	* **Addresses**: `11000000.10101000.00000001.00000000`
	* **Mask**: `11111111.11111111.11111111.00000000`
	* **Hosts**: 256 - 2 = 254
* **Borrow 2** (/26):
	* **Addresses**: `11000000.10101000.00000001`**`.00`**`000000`
	* **Mask**: `11111111.11111111.11111111.`**`11`**`000000`
	* **Hosts**: 64 - 2 = 62 Hosts
		* Note the **`bold IP block`**
		* **SW1**: 
			* **`00`** part:
			* `192.168.1.0/26`
			* Network Address: `192.168.1.0`
			* Broadcast Address: `192.168.1.63`
			* Last Host: `192.168.1.62`
			* First Host: `192.168.1.1`
			* Usable: **62 IP**
		* **SW2**:
			* **`01`** part:
			* `192.168.1.64/26`
			* Network Address: `192.168.1.64`
			* Broadcast Address: `192.168.1.127`
			* Last Host: `192.168.1.126`
			* First Host: `192.168.1.65`
			* Usable: **62 IP**
		* **SW3**:
			* **`10`** part:
			* `192.168.1.128/26`
			* Network Address: `192.168.1.128`
			* Broadcast Address: `192.168.1.191`
			* Last Host: `192.168.1.190`
			* First Host: `192.168.1.129`
			* Usable: **62 IP**
		* **SW4**:
			* **`11`** part:
			* `192.168.1.192/26`
			* Network Address: `192.168.1.192`				
			* Broadcast Address: `192.168.1.255`
			* Last Host: `192.168.1.254`
			* First Host: `192.168.1.193`
			* Usable: **62 IP**
	* ![[img/DAY 13 - Subnetting-6.png]]

### His Attempt:

![[img/DAY 13 - Subnetting-7.png]]