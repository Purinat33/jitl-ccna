**Cisco IOS** = Operating System for Cisco devices

**Interacting with Cisco IOS**: 
1. **Command Line Interface**: More common and is in CCNA
![[img/DAY 4 - Intro to CLI.png]]
2. **Graphical User Interface**: Not a part of CCNA.
   ![[img/DAY 4 - Intro to CLI-1.png]]

<hr>

## Connecting to a Cisco's device

Commonly connect using the device's **Console Port**.

![[img/DAY 4 - Intro to CLI-2.png]]

Using **Rollover Cable** with **DB-9** connector to the PC.
![[img/DAY 4 - Intro to CLI-3.png]]

**Rollover Cable** with **DB-9** connector on the PC end:
![[img/DAY 4 - Intro to CLI-1.jpg]]

Rollover Cable pins:
![[img/DAY 4 - Intro to CLI-2.jpg]]

<hr>

## Connecting to the IOS Terminal

Using a **Terminal Emulator** (eg. *PuTTy*)

![[img/DAY 4 - Intro to CLI-7.png]]

![[img/DAY 4 - Intro to CLI-9.png]]

PuTTy's default setting is the same as Cisco IOS so there's no need to change anything. The settings are beyond the scope of CCNA.

<hr>

## Inside the CLI

Booting up the device for the first time will ask if we want to proceed with the initial configuration dialog. 

![[img/DAY 4 - Intro to CLI-11.png]]

### Mode of operations:
1. **User EXEC Mode**: 
	1. Default mode when entering the terminal.
	2. Indicated by the `>` next to the Host Name.
	    ![[img/DAY 4 - Intro to CLI-13.png | center | 256]]
	3. Very Limited. Users can look at somethings but **cannot** make any changes to the configuration.
	   ![[img/DAY 4 - Intro to CLI-12.png | center]]
2. **Privileged EXEC Mode**:
	1. Seen from the **#** next to the host name.
	2. Access via the `enable` command from **User EXEC Mode**
	   ![[img/DAY 4 - Intro to CLI-14.png | center | 256]]
	3. Provide complete access to view the device's configuration, restarting the device etc.
	4. Cannot change the configuration, but can change the time, save the configuration file etc.
	5. Comparing **User EXEC Mode** commands and **Privileged EXEC Mode** commands:
	   ![[img/DAY 4 - Intro to CLI-15.png]]
	   ![[img/DAY 4 - Intro to CLI-16.png]]
	   <u>Trivia</u>: 
		   * Use the `?` command to view available commands. 
		   * Appending `?` will show available commands containing the prepended strings.
			![[img/DAY 4 - Intro to CLI-17.png | center | 518]]
3. **Global Configuration Mode**
	1. Seen from the **(config)** next to the host name.
	2. Access using `configure terminal` command from the **Privileged EXEC Mode**
	   ![[img/DAY 4 - Intro to CLI-18.png | center | 1024]]
	3. Allows configuration on a *device* scale (not port/interface).
	   ![[img/DAY 4 - Intro to CLI-19.png]]
	4. Allows execution of **Privileged EXEC Mode** commands by adding a `do` command before adding any **Privileged EXEC Mode** commands afterwards. 
	   * eg. `Router(config)# do reload` is the same as `Router# reload`
4. **Sub Configuration Mode**
	1. Allows for configuration on specific interfaces (eg. port)
	2. Accessed from **Global Configuration Mode** and will depend on what we want to set. (Will be covered later. No need to remember these sub-modes right now).
	   ![[img/DAY 4 - Intro to CLI-3.jpg]]
	(Will be covered later. No need to remember these sub-modes right now!)
	
<hr>

### Device's Configuration Files:

Each device have **2 separate configuration files** being stored on the device at the same time.
1. **`running-config`**: The current, active configuration file on the device. As you enter commands in the CLI, you edit the active configuration. Can be viewed using `show running-config` while in **Privileged EXEC Mode** (or `do show running-config` while in **Global Config Mode**). The file is stored in the **RAM** and is lost upon reloading/restarting.
2. **`startup-config`**: Stored in the **NVRAM**, it will be loaded upon starting the device. Viewed using `show startup-config`

To save the running configuration so that it persists, we can either use (while in **Privileged EXEC Mode**):
* `write`
* `write memory`
* `copy running-config startup-config`

<hr>

# Packet Tracer Lab

Configuring a router's security setting.
