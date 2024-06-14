# Variable-Length Subnet Mask

* Up to this point, we've been using **FLSM** (**Fixed-Length Subnet Mask**) for subnetting.
* This means that all of the subnets use the same prefix length & share the same number of hosts. (e.g. Subnetting a Class C network into four subnets *of equal size* using /26)
* **VLSM (Variable-Length Subnet Masks)** is the process of creating subnets of *different sizes*, to make your use of network addresses more efficient.
* **VLSM** is more complicated than FLSM, but doable.
<hr>

## Example:

![[img/DAY 15 - VLSM.png]]

Using **FLSM**, we need to borrow 3 bits to get 8 subnets, which leave each subnet with only 32 IPs (30 Hosts), which is not enough.

<hr>

## Steps:

1. Assign the **Largest Subnet** at the **Start** of the address space.
2. Assign the second-largest subnet after it.
3. Repeat the process until all subnets have been assigned.

### From the Example:

![[img/DAY 15 - VLSM-1.png]]

**Order**:
1. Tokyo LAN A (110)
2. Toronto LAN B (45)
3. Toronto LAN A (29)
4. Tokyo LAN B (8)
5. **Point-to-Point** Connection (2)

<hr>

#### Tokyo LAN A

![[img/DAY 15 - VLSM-2.png]]

* **Network Address**: `192.168.1.0/25`
* **Broadcast Address**: `192.168.1.127/25`
* **First Host**: `192.168.1.1/25`
* **Last Host**: `192.168.1.126/25`
* **No. of Hosts**: 126

#### Toronto LAN B
* **Network Address**: `192.168.1.128/26`
* **Broadcast Address**: `192.168.1.191/26`
* **First Host**: `192.168.1.129/26`
* **Last Host**: `192.168.1.190/26`
* **No. of Hosts**: 62

#### Toronto LAN A
* **Network Address**: `192.168.1.192/27`
* **Broadcast Address**: `192.168.1.223/27`
* **First Host**: `192.168.1.193/27`
* **Last Host**: `192.168.1.222/27`
* **No. of Hosts**: 30

#### Tokyo LAN B
* **Network Address**: `192.168.1.224/28`
* **Broadcast Address**: `192.168.1.239/28`
* **First Host**: `192.168.1.225/28`
* **Last Host**: `192.168.1.238/28`
* **No. of Hosts**: 14
	* Using `/29` gives 8 addresses but **6** usable addresses.

#### Point-to-Point Connection:
* **Network Address**: `192.168.1.240/31`
* **Broadcast Address**: `192.168.1.241/31`
* **First Host**: `192.168.1.240/31` (**R1**)
* **Last Host**: `192.168.1.241/31` (**R2**)
* **No. of Hosts**: 0
	* But this is for **Point-to-Point** connection, where exactly **Two IPs** are valid. 

##### BUT... `/31` is generally *discouraged* for CCNA.

#### Point-to-Point Connection (CCNA):
* **Network Address**: `192.168.1.240/30`
* **Broadcast Address**: `192.168.1.243/30`
* **First Host**: `192.168.1.241/30`
* **Last Host**: `192.168.1.242/30`
* **No. of Hosts**: 2

![[img/DAY 15 - VLSM-3.png]]

<hr>

## Additional Practice:

* [http://www.subnettingquestions.com](http://www.subnettingquestions.com)
* [http://subnetting.org](http://subnetting.org)
* [https://subnettingpractice.com](https://subnettingpractice.com)
<hr>