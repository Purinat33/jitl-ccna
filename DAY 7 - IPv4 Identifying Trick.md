# IPv4 Identifying Tips & Tricks:

#### [Playlist on Subnetting from Practical Networking](https://youtube.com/playlist?list=PLIFyRwBY_4bQUE4IB5c4VPRyDoLgOdExE&si=cdsNEXcZFWVlVmFB)

## Question:

Finding important IP Addresses given an IPv4 address:
1. **Network Address**: Make all Host portion = `0`
2. **Broadcast Address**: Make all Host portion = `1`
3. **First Usable Host**: The address after network address.
4. **Last Usable Host**: The address before broadcast address.
5. **No. of Usable Host**: *big math?* 

We know how to, but would we really convert decimal to binary and back to decimal again?
* eg. `10.0.0.4/9`:

|   **Octet**    |   1<sup>st   |   2<sup>nd   | 3<sup>rd | 4<sup>th |
| :------------: | :----------: | :----------: | :------: | :------: |
| **IP Address** | **00001010** | **0**0000000 | 00000000 | 00000100 |
|    **Mask**    | **11111111** | **1**0000000 | 00000000 | 00000000 |
* Network Address:
  
|  **Octet**  | 1<sup>st |   2<sup>nd   |   3<sup>rd   |   4<sup>th   |
| :---------: | :------: | :----------: | :----------: | :----------: |
| **Binary**  | 00001010 | 0**0000000** | **00000000** | **00000000** |
| **Decimal** |    10    |      0       |      0       |      0       |
* Broadcast Address
  
|  **Octet**  | 1<sup>st |   2<sup>nd   |   3<sup>rd   |   4<sup>th   |
| :---------: | :------: | :----------: | :----------: | :----------: |
| **Binary**  | 00001010 | 0**1111111** | **11111111** | **11111111** |
| **Decimal** |    10    |     127      |     255      |     255      |

We would ran out of time in any exam before we can do anything.

<hr>

## The Answer (Table):

1. Create a table of the "*powers of 2*" from 1 to 128, call this row the `Group Size`:

| **Group Size** | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| :------------- | :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
2. Subtract from **256** on each column, this row is called the `Mask`:
   
| **Group Size** | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| :------------- | :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| **Mask**       | 128 | 192 | 224 | 240 | 248 | 252 | 254 | 255 |
3. Now write the Netmask `/x` notation (**CIDR**) from `/32` from **Right to left** and **Top to Bottom**, each row will correspond to the **4th**, **3rd**, **2nd**, **1st** **Octet** respectively.

| **Group Size** | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| :------------- | :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| **Mask**       | 128 | 192 | 224 | 240 | 248 | 252 | 254 | 255 |
| **4<sup>th**   | /25 | /26 | /27 | /28 | /29 | /30 | /31 | /32 |
| **3<sup>rd**   | /17 | /18 | /19 | /20 | /21 | /22 | /23 | /24 |
| **2<sup>nd**   | /9  | /10 | /11 | /12 | /13 | /14 | /15 | /16 |
| **1<sup>st**   | /1  | /2  | /3  | /4  | /5  | /6  | /7  | /8  |

4. Number of **Usable Host** is `pow(2, 32-netmask) - 2` (+2 when including network and broadcast address)
<hr>

## The Answer (How to use Table):

<u>eg:</u> From the same question: `10.0.0.4/9`

1.  Seeing the `/9` we look for the specific cell in the Table.
  
| **Group Size** | 128              | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| :------------- | :--------------- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| **Mask**       | 128              | 192 | 224 | 240 | 248 | 252 | 254 | 255 |
| **4<sup>th**   | /25              | /26 | /27 | /28 | /29 | /30 | /31 | /32 |
| **3<sup>rd**   | /17              | /18 | /19 | /20 | /21 | /22 | /23 | /24 |
| **2<sup>nd**   | <u><b>/9</b></u> | /10 | /11 | /12 | /13 | /14 | /15 | /16 |
| **1<sup>st**   | /1               | /2  | /3  | /4  | /5  | /6  | /7  | /8  |
	* `/9` is associated with the 2nd octet.
	* Looking at the 2nd octet, we set that octet (and the 3rd & 4th octet) to `0` then **increment** the original 2nd octet by the **Group Size** until the value of the 2nd octet is **Greater than or equal** the **Original**'s 2nd octet. 
		* (Increment must happened at least once even if the set-0 of that octet is already `0`)

| Octet             | 1<sup>st | 2<sup>nd | 3<sup>rd | 4<sup>th | Contain 0? |
| ----------------- | -------- | -------- | -------- | -------- | ---------- |
| **Original**      | 10       | 0        | 0        | 4        | -          |
| **2nd Octet = 0** | 10       | 0        | 0        | 0        | -          |
| **+ Group Size**  | -        | 128      | -        | -        | YES        |

* We see that 128 has surpassed the original 2nd octet's value of `0`:
	* `10.128.0.0` is the result **but** we need to back down by 1 address to `10.127.255.255` as the broadcast address.
	* `10.0.0.0` is the result *before* the 128 increment, and thus that is the network address.
* We can also convert between `/9` format and the mask's dotted decimal notation:
	* Mask value of the `/9` column is 128, and so the mask is `255.128.0.0`
* Usable IP = `pow(2, 32-9) - 2` = 8388606 IP Addresses.

<hr>

### Eg: `172.16.26.5/22` 

| **Group Size** | 128 | 64  | 32  | 16  | 8   | 4         | 2   | 1   |
| :------------- | :-- | :-- | :-- | :-- | :-- | :-------- | :-- | :-- |
| **Mask**       | 128 | 192 | 224 | 240 | 248 | 252       | 254 | 255 |
| **4<sup>th**   | /25 | /26 | /27 | /28 | /29 | /30       | /31 | /32 |
| **3<sup>rd**   | /17 | /18 | /19 | /20 | /21 | ***/22*** | /23 | /24 |
| **2<sup>nd**   | /9  | /10 | /11 | /12 | /13 | /14       | /15 | /16 |
| **1<sup>st**   | /1  | /2  | /3  | /4  | /5  | /6        | /7  | /8  |

* `/22` deals with the *3rd* octet.

|              | 1st | 2nd | 3rd      | 4th | Contains 26? |
| ------------ | --- | --- | -------- | --- | ------------ |
| Original IP  | 172 | 16  | 26       | 5   | -            |
| Set 3rd = 0  | 172 | 16  | 0        | 0   | -            |
| + Group Size | -   | -   | 4        | -   | No           |
| + Group Size | -   | -   | 8        | -   | No           |
| + Group Size | -   | -   | 12       | -   | No           |
| + Group Size | -   | -   | 16       | -   | No           |
| + Group Size | -   | -   | 20       | -   | No           |
| + Group Size | -   | -   | ***24*** | -   | No           |
| + Group Size | -   | -   | ***28*** | -   | YES          |
* Original value of the 3rd octet is `26` and from the table, we can see that it lies between `24` and `28`.
	* `28` in the 3rd octet gives: `172.16.28.0` back down by 1 gives the **Broadcast Address** of `172.16.27.255`. 
	* `24` in the 3rd octet gives: `172.16.24.0` gives us the **Network Address**.
* Mask in dotted-decimal notation: `255.255.252.0`
* Number of usable hosts: `pow(2, 32-22) - 2` = **1022** IP
  
<hr>

### Eg: `192.168.1.186/26` 

| **Group Size** | 128 | 64      | 32  | 16  | 8   | 4   | 2   | 1   |
| :------------- | :-- | :------ | :-- | :-- | :-- | :-- | :-- | :-- |
| **Mask**       | 128 | 192     | 224 | 240 | 248 | 252 | 254 | 255 |
| **4<sup>th**   | /25 | **/26** | /27 | /28 | /29 | /30 | /31 | /32 |
| **3<sup>rd**   | /17 | /18     | /19 | /20 | /21 | /22 | /23 | /24 |
| **2<sup>nd**   | /9  | /10     | /11 | /12 | /13 | /14 | /15 | /16 |
| **1<sup>st**   | /1  | /2      | /3  | /4  | /5  | /6  | /7  | /8  |

`/26` is 4th octet.

|              | 1st | 2nd | 3rd | 4th | Contains 26? |
| ------------ | --- | --- | --- | --- | ------------ |
| Original IP  | 192 | 168 | 1   | 186 | -            |
| Set 4th = 0  | 192 | 168 | 1   | 0   | -            |
| + Group Size | -   | -   | -   | 64  | No           |
| + Group Size | -   | -   | -   | 128 | No           |
| + Group Size | -   | -   | -   | 192 | Yes          |
* **Broadcast Address**: `192.168.1.192` back down by 1 equals `192.168.1.191`
* **Network Address**: `192.168.1.128` 
* **First Host**: `192.168.1.129`
* **Last Host**: `192.168.1.190`
* **Mask**: `/26` equals `255.255.255.192`
* **No. of Hosts**: `pow(2, 32-26) - 2` = 62 IP.
  
  <hr>