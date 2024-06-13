# Subnetting Practices

## `192.168.255.0/24` into **5** subnets:
* **Original**:
	* `11000000.10101000.11111111.00000000`
	* `11111111.11111111.11111111.00000000`
	*  Borrow **3** bits from the host portion (/27):
		* `11111111.11111111.11111111`**`.111`**`00000`
* **S1**:
	* Borrowed bits = `000`
	* Network ID: `00000` = `192.168.255.0`
	* Broadcast: `11111` = `192.168.255.31
* **S2**:
	* Borrowed bits = `001`
	* Network: `192.168.255.32`
	* Broadcast: `192.168.255.63`
* **S3**:
	* Borrowed bits = `010`
	* Network: `192.168.255.64`
	* Broadcast: `192.168.255.95`
* **S4**:
	* Borrowed bits = `011`
	* Network: `192.168.255.96`
	* Broadcast: `192.168.255.127`
* **S5**:
	* Borrowed bits = `100`
	* Network: `192.168.255.128`
	* Broadcast: `192.168.255.159`


* **Formula**: 
	* No. of subnets = `pow(2, borrowed_bits)`: borrow 3 bits = 8 subnets. 
	* (Don't subtract 2 like No. of Hosts formula)


<hr>

## What subnet does host `192.168.5.57/27` belong to?

* `192.168.5.57` into `11000000.10101000.00000101`**`.001`**`11001`/27

| Network | Host  | Mask |
| ------- | ----- | ---- |
| **001** | 00000 | /27  |
| **32**  | 0     | /27  |
**Answer**: Subnet `192.168.5.32/27`

<hr>

## What subnet does host `192.168.29.219/29` belong to?

* Last octet: `219` = `11011011`

| Network | Host | Mask |
| ------- | ---- | ---- |
| 11011   | 011  | /29  |
| 216     | 0    | /29  |
**Answer**: Subnet `192.168.29.216/29`

**Note**: The process is exactly the same regardless of classes.

<hr>

## Create 80 Subnets from `172.16.0.0/16`, what prefix to use?

* **Mask**: `1111111.11111111.00000000.00000000`
* **Borrowing 7 Bits** (/23):
	* `pow(2, 7)` = 128 Subnets >= 80 Subnets requirement.
* **New Mask**: 
	* `11111111.11111111.11111110.00000000`
	* `255.255.254.0`

**Answer**: Prefix Length = 23

<hr>

## `172.22.0.0/16` into 500 Subnets

* **Mask**: `1111111.11111111.00000000.00000000`
* **Borrowing 9 Bits** (/25):
	* `pow(2, 9)` = 512 Subnets >= 500 Subnets requirement.
* **New Mask**: 
	* `11111111.11111111.11111111.10000000`
	* `255.255.255.192`

**Answer**: /25

<hr>

## 10.0.0.0/8 into 1,000,000 subnets

* **Mask**:  `1111111.00000000.00000000.00000000`
* **Borrowing 20 Bits** (/28):
	* `pow(2, 20)` = 1,048,576 Subnets >= 1,000,000 Subnets requirement.
* **New Mask**: 
	* `11111111.11111111.11111111.11110000`
	* `255.255.255.232`

<hr>

## 172.25.217.192/21 Belongs to?

* **Address**: `10101100.00011001.11011001.11000000`
* **Host = 0**: `10101100.00011001.11011` **`000.00000000`**
	* `172.25.216.0/21`

**Answer**: `172.25.216.0/21`

<hr>

## Broadcast IP of `192.168.91.78/26`

* **Address**: `11000000.10101000.01011011.01001110`
* **Separate Network/Host**: `11000000.10101000.01011011.01` & **`001110`**
* **Host = 1**: 
	* `192.168.91.01` & **`111111`**
	* `192.168.91.01111111`
**Answer** `192.168.91.127`

<hr>