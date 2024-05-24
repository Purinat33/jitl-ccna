# Switch Interface

![[img/DAY 9 - Switch Interfaces.png]]

## Viewing Interfaces:

From SW1:

* **Viewing** SW1's interface (Same command as router): `show ip interface brief`

![[img/DAY 9 - Switch Interfaces-1.png]]

* None of the interfaces have no **IP Assignment** because a **Switch is a Layer 2 Device** while IP Address is a **Layer 3 Addressing**.
	* There are reasons to assign IP Addresses to Switch's interfaces, but that comes later.
* **Router vs. Switch Interfaces**:
	* **Router** interfaces have the `shutdown` command applied by default (*`administratively down/down`* State)
	* **Switch** interfaces **DO NOT** have the `shutdown` command applied by default.
		* Will be in the *`up/up`* state if connected to another device.
		* Will be in the *`down/down`* state if **NOT** connected to another device.
* **View Speed and Duplex of each interface** via `show interfaces status`
	![[img/DAY 9 - Switch Interfaces-4.png | center]]
	* **Name**: Description of an interface.
	* **Status**: *Connected* or *Not Connected* 
	* **VLAN**: Will be covered later.
	* **Duplex**: Direction of sending/receiving data.
	* **Speed**: Depend on the **Speed of the slower of the two** (The interface *vs.* The device connecting to that interface).
		* eg: **10 Mbps** device connecting to the **100 Mbps** port will make the communication speed of this conncetion = **10 Mbps**.
	* **Type**: `10` (**Ethernet**, Slower than **Fa**) and `100` (**Fast Ethernet** or **Fa**)
		* No `1000` or `10G` since these are **Fa** (**Fast Ethernet**) interfaces an not **G** (**Gigabit Ethernet**)

### Duplex:

![[img/DAY 9 - Switch Interfaces-5.png]]

* **Full Duplex**: 
	* The device *can send and receive data* **AT THE SAME TIME**, it does not have to wait. (Most Modern Devices have this capabilities.)
* **Half Duplex**:
	* The device *cannot send and receive* data at the same time.
	* If it is receiving a frame, it must **wait** before sending a frame.
	* eg: **Hub** 

#### Hub:
![[img/DAY 9 - Switch Interfaces-6.png]]

* Is considered to be a **Layer 1 Device** instead of Layer 2 because it performs similar function to *switches* (**Frame Routing**) but **without** the use of any **MAC Addressing** or **MAC Table**. 
* More similar to a networking *repeater*.
* Will **Always Flood** the frames regardless of the frame's type.
* Devices connected to a Hub must always operate in **Half-Duplex** mode.
* Have a mechanism to deal with collisions called **CSMA/CD**.

![[img/DAY 9 - Switch Interfaces-8.png]]

#### CSMA/CD in 

![[img/DAY 9 - Switch Interfaces-7.png]]

* <u><b>C</b></u>arrier <u><b>S</b></u>ense <u><b>M</b></u>ultiple <u><b>A</b></u>ccess *with* <u><b>C</b></u>ollision <u><b>D</b></u>etection
* Used in Half-Duplex situation (like **Hub** network) to deal with collisions.
* Before sending frames, devices ***LISTEN*** to the **Collision Domain** until they detect that other devices are not sending.
* If a **Collision** does occur, the device sends a jamming signal to inform the other devices that a collision happened.
* Each device will wait *a random period of time* before sending frames again.

#### Collision Domain in Switches

![[img/DAY 9 - Switch Interfaces-10.png]]
* As established, **Switches** are considered a **Layer 2 Device** due to usage of **MAC Addressing**, **Frame Forwarding** etc.
* Collisions *rarely* occur (More of a configuration fault rather than normal usual occurrences like in Hub)
* Devices connected to a Switch can operate in **Full-Duplex** mode.
### Speed:

![[img/DAY 9 - Switch Interfaces-9.png]]

<hr>
## Auto-negotiation

* Interfaces that can run at different speeds (**10/100** or **10/100/1000** have default settings of `speed auto` and `duplex auto`
* Interfaces **advertise** their capabilities to the neighboring device, and they negotiate the best `speed` and `duplex` settings they are capable of.
  
![[img/DAY 9 - Switch Interfaces-11.png]]

![[img/DAY 9 - Switch Interfaces-12.png]]

![[img/DAY 9 - Switch Interfaces-13.png]]

### What if auto-negotiation is disabled on the device connected to the Switch?

* **Speed**: The switch will try to sense the speed that the device is operating at.
	* If it fails to sense the speed, it will use the **slowest supported speed** 
	* eg. **10 Mbps** on a **10/100/1000** Interface
* **Duplex**:
	* If the speed is **10 or 100** Mbps, the switch will use **Half-Duplex**.
	* If the speed is **1000 Mbps** or greater, the switch will use **Full-Duplex**. 
![[img/DAY 9 - Switch Interfaces-14.png]]

<hr>

## Interfaces Error

* `show interfaces {interface-name}` (Like routers).
![[img/DAY 9 - Switch Interfaces-15.png]]

* Interesting statistics (Routers have similar statistics):
![[img/DAY 9 - Switch Interfaces-16.png]]
	* **Runts**: Frames that are *Smaller* than the minimum Frame size (*64 Bytes*)
	* **Giants**: Frames that are *Larger* than the maximum Frame size (*1518 Bytes*)
	* **CRC**: Frames that failed the CRC Check (*Ethernet FCS trailer*)
	* **Frame**: Frames that have an incorrect format (due to errors)
	* **Input Errors**: Total of various counters, including the above four.
	* **Output Errors**: Frames the switch tried to send but failed due to errors.

<hr>

# Summary

![[img/DAY 9 - Switch Interfaces-4.png | center]]

* View switch's interfaces using `show interfaces status`
	* Each interface do not have `shutdown` applied by default (**No `administratively down` like Routers**).
	* Will be in `up/up` state if connected to another device.
	* Be in `down/down` state if not connected.
	* **Duplex**: `Full`, `half`, or `auto`
	* **Speed**: Depends on the *slower* speed of either the interface or the device connected to the interface.
	* **Type**: Slower speeds than the interface and up-to-and-including the speed of the interface. (100Mbps Interface includes both 10Mbps and 100Mbps **but** not 1000Mbps)

![[img/DAY 9 - Switch Interfaces-17.png]]

* View specific switch interface's detail using `show interfaces {interface-name}`
	* **Runts**: Smaller than **64** Bytes (Minimum)
	* **Giants**: Larger than **1518** Bytes (Maximum)
	* **CRC**: Failed CRC Check
	* **Frame**: Incorrect Format
	* **Input Error**: Total Counters
	* **Output Error**: Switch failed to send

* **Duplex**: Direction of data communication.
	* **Full**: Send and Receive at the same time (eg. **SWITCH** networks).
	* **Half**: Must wait before sending (eg. **HUB** networks)
		* **HUB**: 
			* Considered to be a *Layer 1* device due to no MAC address nor table being used. 
			* Will **always broadcast frames** regardless of type.
			* **Collisions** common.
		* **CSMA/CD**:
			* Used in **Half-Duplex** situation.
			* <u><b>C</b></u>arrier <u><b>S</b></u>ense <u><b>M</b></u>ultiple <u><b>A</b></u>ccess *with* <u><b>C</b></u>ollision <u><b>D</b></u>etection
			* Devices *listen* to the collision domain.
			* If a collision occur, the device sends a jamming signal to the collision domain.
			* Each device waits a random period of time before resending frames again.

![[img/DAY 9 - Switch Interfaces-7.png]]

* **Auto-Negotiation** (`speed` and `duplex`):
	* Interfaces usually can run at different speeds (**10/100** or **10/100/1000**) have default settings of `speed auto` and `duplex auto`.
	* Interfaces **advertise** their capabilities to connected device and negotiate the `speed` and `duplex`.
	* **If Auto-Negotiation is Disabled**:
		* **Speed**: 
			* Try sensing the speed the connected device is operating at. If failed, it uses the *slowest supported speed*. (**10Mbps** on a **10/100/1000** Interface)
		* **Duplex**: 
			* Speed of **10 or 100Mbps**, the switch uses **Half-Duplex**.
			* Speed of **1000Mbps** or higher, the switch uses **Full-Duplex**.

<hr>