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
![[img/DAY 4 - Intro to CLI-20.png]]

## Tasks:
1. Change the hostnames of the router and switch to the appropriate names (R1, SW1)
   ![[img/DAY 4 - Intro to CLI-21.png | center | 518]]
   ![[img/DAY 4 - Intro to CLI-22.png | center | 518]]
2. Configure an unencrypted enable password of 'CCNA' on both devices.
   ![[img/DAY 4 - Intro to CLI-23.png | center | 518]]
3. Exit back to user EXEC mode and test the password.
   ![[img/DAY 4 - Intro to CLI-24.png | center | 518]]
   <u>Note</u>: Password typed aren't visible (but it's there).
4. View the password in the running configuration.
   ![[img/DAY 4 - Intro to CLI-25.png | center | 518]]
5. Ensure that the current password, and all future passwords, are encrypted.
   ![[img/DAY 4 - Intro to CLI-26.png | center | 518]]
6. View the password in the running configuration.
   ![[img/DAY 4 - Intro to CLI-27.png | center| 518]]
   <u>Note</u>: `7` is Cisco's encryption algorithm (but weak)
   * Removing/undoing encryption with `no` command (Will apply on next password being set):
    ![[img/DAY 4 - Intro to CLI-28.png | center | 518]]
7. Configure a more secure, encrypted enable password of 'Cisco' on both devices
   ![[img/DAY 4 - Intro to CLI-29.png | center | 518]]
8. Exit back to user EXEC mode and then return to privileged EXEC mode. 
	1. Which password do you have to use?
	   * Password is `Cisco`
	   ![[img/DAY 4 - Intro to CLI-30.png | center | 512]]
9. View the passwords in the running configuration.
	1. What encryption type number is used for the encrypted `enable password`? `7` (weak)
	2. What encryption type number is used for the encrypted `enable secret`? `5` (Stronger)
10. Save the running configuration to the startup configuration
    ![[img/DAY 4 - Intro to CLI-31.png | center | 512]]

<hr>

# Summary:

**Connecting to the device:**
1. Connect to a Cisco's device using the device's console port
2. **Rollover Cable** with a **DB-9** Connector

**Mode of Operations**:
```mermaid
flowchart LR
A[User EXEC] -- "`**enable**`" --> B[Privileged EXEC]
B--"`**configure terminal**`" --> C[Global Configuration]

style A fill:#b1b7b4,stroke:red,stroke-width:4px
style B fill:#b1b7b4,stroke:red,stroke-width:4px
style C fill:#b1b7b4,stroke:red,stroke-width:4px
```
**Commands**:
1. **User EXEC Mode**:
	1. `enable`: Enter **Privileged EXEC Mode**
2. **Privileged EXEC Mode**:
	1. `configure terminal`: Enter **Global Configuration Mode**
	2. `show ...` (eg. `show running-config`, `show startup-config`): View device's configuration detail. 
	3. `write`, `write memory`, `copy running-config startup-config`: Save the current configuration to startup configuration when device is booted.
3. **Global Configuration Mode**:
	1. `do ...` (eg. `do show running-config`): Execute **Privileged EXEC Mode** commands while in this mode.
	2. `hostname ...` (eg. `hostname R1`): Set device's hostname.
	3. `enable password ...` (eg. `enable password CCNA`): 
		1. Set password for entering **Privileged EXEC Mode**
		2. Password will be in plaintext in config files.
	4. `service password-encryption`: Type-`7` encrypt the once-plaintext password shown in config files.
	5. `no ...` (eg. `no service password-encryption`): undo/cancel commands. Will not decrypt currently encrypted password.
	6. `enable secret ...` (eg. `enable secret Cisco`)
		1. Set password for entering **Privileged EXEC Mode**
		2. Password automatically encrypted (Type-`5`) when viewing config files.
		3. Make `enable password ...` unusable.

**Shortcuts**:
Appending `?` to partially written commands show possible autocomplete (eg. `en?` displays `enable` in **User EXEC**). Thus, we can abbreviate commands like:
* `enable`:
  ![[img/DAY 4 - Intro to CLI-34.png | center | 512]]
*  `configure terminal`: 
![[img/DAY 4 - Intro to CLI-35.png | center | 512]]
* `show running-config`:
  ![[img/DAY 4 - Intro to CLI-36.png | center| 512]]
  <hr>