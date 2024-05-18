# OSI Model & TCP/IP Suite
Networking models help categorize and provide a structure for networking **protocols** and **standards**.

**Encapsulation/De-Encapsulation**:
![[img/DAY 3 - OSI Model & TCP IP Suite-1.png]]
* The act of adding header and/or trailer to the data - **Encapsulation**
* The act of removing header and/or trailer to expose data - **De-Encapsulation**

**Same Layer vs. Adjacent Layer Interaction**:
![[img/DAY 3 - OSI Model & TCP IP Suite-2.png]]
* **Same Layer Interaction** works on the same layer between 2 Hosts (Network layer to Network layer).
* **Adjacent Layers Interaction** works by having a layer supplying service to the layer directly adjacent to it (eg. Encapsulation, Header attachment)

**Protocol Data Unit (PDU)**:
The basic unit of data for each layer.
## OSI Model
* Short for **Open Systems Interconnection**
* Created by the International Organization for Standardization (**ISO**)
![[img/DAY 3 - OSI Model & TCP IP Suite.png]]

### Layers (From Top to Bottom):
7. **Application Layer**
	1. Closest to the end user.
	2. Interacts with software applications (Not the software itself)
	3. **HTTP, HTTPS, DNS** etc.
	4. Identify communication partner.
	5. Synchronizing Communication.
6. **Presentation Layer**
	1. Translate data into Application Layer's format. (Bits to jpeg, mp4 etc.)
	2. Encryption & Decryption
5. **Session Layer**: 
	1. Controls dialogues (Sessions) between communicating hosts.
	2. Establishes, manages, terminates connections between the **local application** (Browser) and **remote application** (Youtube).
> Network Engineers don't really work with the Top-3 Layers.

4. <u><b>Transport Layer</b></u>:
	1. <u><b>Segments</b> large data into smaller data and reassemble data back.</u> for easier transmission than 1 large data at once.
	2. Provides **Host-to-Host** (**_Process-to-Process_** is also a popular methodology) communication.
	3. Add *Layer 4 Header* to the data during encapsulation.
	4. L4 PDU = **Segment**
3. <u><b>Network Layer</b></u>:
	1. Provides connectivity between *end-hosts* **on different networks** (eg. outside of the LAN)
	2. Provide **End-to-End** communication.
	3. Provide **Logical Addressing (IP Addresses)**
	4. Layer 3 device: **Router**
	5. L3 PDU = **Packet**
2. <u><b>Data Link Layer</b></u>:
	1. Provide **Hop-to-Hop**/**Node-to-Node** communication.
	2. Defines how data is formatted for transmission over a physical medium (eg. copper UTP cables)
	3. **Detects and corrects Physical Layer errors**
	4. Provide **Physical Addressing (MAC Addresses)**
	5. Layer 2 device: **Switch**
	6. L2 PDU = **Frame** 
1. <b><u>Physical Layer</u></b>:
	1. Define physical characteristics of the medium used to transfer. (eg. Voltage Level, Maximum Transmission Distances, Physical Connectors, Cable etc.)
	2. Digital bits are converted to electrical (wired) or radio (wireless)
	3. Information from [DAY 2 - Interfaces and Cables](https://youtu.be/ieTH5lVhNaY) are related to this layer.

![[img/DAY 3 - OSI Model & TCP IP Suite.jpg]]
**Process, Host, Node-to-Node visualization**

<hr>

## TCP/IP Suite

* A conceptual model and set of communication protocols used in the Internet and other networks.
* Known as **TCP/IP** because those are two of the foundational protocols of the suite.
* Developed by the United States Department of Defense through *DARPA* (Defense Advanced Research Projects Agency)
* Similar to the **OSI Model**, but with fewer layers.
* This is the model actually in use in modern networks.
![[img/DAY 3 - OSI Model & TCP IP Suite-3.png | center]]

(Note that the OSI model still influences how network engineers think and talk about networks. ) 
* People still mostly refer to the OSI Model when talking in <u>Number</u> (eg. **Layer 2 Problem** = **Data Link Layer Problem**)
* TCP/IP model might have different layout/naming based on where you look.
  ![[img/DAY 3 - OSI Model & TCP IP Suite-4.png]]

<hr>

# Summary:

**Model Comparisons**

![[img/DAY 3 - OSI Model & TCP IP Suite-5.png]]

**Protocol Data Unit (PDU)**

![[img/DAY 3 - OSI Model & TCP IP Suite-6.png]]

**Layers**:
* **Application**: 
	* Defines how applications like Mails or Websites will operate.
	* Process-to-Process communication.
	* Identify communication partner.
	* **HTTP, HTTPS, DNS** etc.
* **Presentation**:
	* Format data for Application Layer (image, video, text etc.)
* **Session**:
	* Session establishment, maintenance, and termination
* <u><b>Transport</b></u>:
	* **Host-to-Host** communication.
	* **Segmentation/Reassembling** of data. 
	* **TCP, UDP**
	* Addressing: **Port Numbers**
* <u><b>Network</b></u>:
	* **End-to-End** communication.
	* **Routing** 
	* Devices: **Routers** 
	* Addressing: **IP Addresses**
* <u><b>Data Link</b></u>:
	* **Node-to-Node** communication
	* Format data for physical medium transmission.
	* **Detects and corrects Physical Layer errors**
	* Devices: **Switches**
	* Addressing: **MAC Addresses**.
	* The only layer with a Trailer in addition to a Header.
* <u><b>Physical</b></u>:
	* Physical medium transmission (eg. UTP Cabling)
	* Electrical or Radio signals.
	* Devices: **Hub, Repeater**

<hr>