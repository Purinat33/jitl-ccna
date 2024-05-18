# Interfaces and Cables

![[img/DAY 2 - Interfaces and Cables.png]]

## Questions:

Take a look at the switch: 
1. What are `10Base-T`, `100Base-T`, `1000Base-T`, and `auto-MDIX`?
2. What are used to plug into the switch ports?
3. What type of cables are used?

## Answer:

### The answers are all related to the "<b><u>Ethernet</u></b>" ***Important***

* **Ethernet** is a <u>collection</u> of network protocols and standards. For now we will only focus on the **cabling** Ethernet standards.

#### Ethernet **Cabling** Standards 

Are defined in the **IEEE 802.3** (IEEE = `Institude of Electrical and Electronics Engineers`)

<hr>

Ethernet Standards (**Copper**): ***REMEMBER!***

| Speed     | Common Name         | IEEE Standards | Informal Name | Maximum Length |
| --------- | ------------------- | -------------- | ------------- | -------------- |
| 10 Mbps   | Ethernet            | 802.3i         | 10Base-T      | 100m           |
| 100 Mbps  | Fast Ethernet       | 802.3u         | 100Base-T     | 100m           |
| 1000 Mbps | Gigabit Ethernet    | 802.3ab        | 1000Base-T    | 100m           |
| 10 Gbps   | 10 Gigabit Ethernet | 802.3an        | 10GBase-T     | 100m           |
<u>Trivia</u>:
	* `100Base-T`
		* 100 = Speed (*100 Mbps*)
		* Base = Baseband Signaling (<u>Outside the scope of CCNA</u>)
		* **T** = Twisted Pair cabling

The cables are joined with **RJ-45** connectors, which can be plugged into devices' ports.

![[img/DAY 2 - Interfaces and Cables-1.jpg]]
An RJ-45 connector.

![[img/DAY 2 - Interfaces and Cables.jpg]]
An RJ-45 joined with an ethernet cable being plugged into a switch.

<hr>

#### UTP Cabling (Unshielded Twisted Pair)
<br>

![[img/DAY 2 - Interfaces and Cables-3.jpg]]
Contains 8 copper wires (4 pairs):
* Wiring Usage:
	1. `10Base-T` and `100Base-T`: Use **2 pairs** of wires.
	2. `1000Base-T` and `10GBase-T`: Use **All pairs** of wires.<br>

##### `10Base-T` and `100Base-T`: <br>

Uses Pin **1,2** and **3,6** in Transmission (*Tx*) and Receiving (*Rx*).
![[img/DAY 2 - Interfaces and Cables-5.png]]
According to the diagram: 
* PC transmits on **Pin 1,2** and Receives on **Pin 3,6**.
* Switch transmit on **Pin 3,6** and Receives on **Pin 1,2**.

![[img/DAY 2 - Interfaces and Cables-6.png]]
According to the diagram: 
* Router transmits on **Pin 1,2** and Receives on **Pin 3,6**.
* Switch transmit on **Pin 3,6** and Receives on **Pin 1,2**.

Devices with transmission and receiving on different pairs use **Straight-Through** cabling.

<hr>

*Q*: What about devices that both transmit and receive on the same pair? (eg. 2 PC)
![[img/DAY 2 - Interfaces and Cables-7.png]]

*A*: We connect transmission pins to receiving pins of the other device, and vice-versa.
![[img/DAY 2 - Interfaces and Cables-8.png]]
Devices with transmission and receiving on the same pairs use **Crossover** cabling.

<hr>

###### 10Base-T and 100Base-T pins usage:

| Transmits on PIN 1,2  | Transmits on PIN 3,6 |
| --------------------- | -------------------- |
| PC                    | Hub                  |
| Router                | Switch               |
| Wireless Access Point |                      |
| Firewall              |                      |

Traditionally devices must be connected correctly using either **Straight-Through Cable** or **Crossover Cable**, else the connection will not be established.

Though modern devices possess **Auto MDI-X** capability, which automatically detects when either type of cables is used and will change/switch `Tx` and `Rx` pins if needed.

<hr>

##### `1000Base-T` and `10GBase-T` cabling <br>

All 8 wires (4 pairs) are used. Each wire is bidirectional.

![[img/DAY 2 - Interfaces and Cables-9.png]]

<hr>

#### Fiber Optics <br>

In addition to **RJ-45** ports on devices, modern devices have **SFP** ports as well. (SFP = **Small Form Pluggable**)

![[img/DAY 2 - Interfaces and Cables-10.png]]

Ports for SFP (Orange)

![[img/DAY 2 - Interfaces and Cables-4.jpg | center | 256]]

Fiber optic cables are then connected to the SFP

![[img/DAY 2 - Interfaces and Cables-5.jpg | center | 400]]

Transmission and Receiving on Fiber Optic cables.

![[img/DAY 2 - Interfaces and Cables.gif]]

Instead of copper + electricity, Fiber Optic uses *fiber glass* + *light beam*
![[img/DAY 2 - Interfaces and Cables-11.png]]

##### 2 Types of Fiber Optic Cables:
1. **Single-Mode**: ![[img/DAY 2 - Interfaces and Cables-12.png]]
	* Thinner core diameter than Multi-Mode
	* Light enters at a single angle (Mode) from a laser-based transmission.
	* Allows longer cables than both UTP and Multi-Mode fiber.
	* More expensive than multi-mode fiber (laser-based transmitter)
2. **Multi-Mode**:![[img/DAY 2 - Interfaces and Cables-13.png]]
	* Core diameter is wider than single-mode fiber.
	* Allows multiple angles (Modes) of light waves to enter the code.
	* Allows longer cable than UTP but shorter than single-mode.
	* Cheaper than Single-Mode fiber. (LED-based transmitter).

<hr>

Ethernet Standards (**Fiber**): ***REMEMBER!***

| Speed   | Common Name         | IEEE Standards | Informal Name | Maximum Length |
| ------- | ------------------- | -------------- | ------------- | -------------- |
| 1 Gbps  | Ethernet            | 802.3i         | 10Base-T      | 100m           |
| 10 Gbps | Fast Ethernet       | 802.3u         | 100Base-T     | 100m           |
| 10 Gbps | Gigabit Ethernet    | 802.3ab        | 1000Base-T    | 100m           |
| 10 Gbps | 10 Gigabit Ethernet | 802.3an        | 10GBase-T     | 100m           |
<u>Trivia</u>: