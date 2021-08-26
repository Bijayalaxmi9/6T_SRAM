


> Written with [StackEdit](https://stackedit.io/).
# 6T SRAM
## Table of Contents:

 - [Overview](##Overview)
 - [Sizing & Modes of Operations](##Sizing_&_Modes_of_Operations)
 - [Pre-layout](##Pre-layout)
	 - [DC Analysis](##DC_Analysis)
	 - [Hold SNM](##Hold_SNM)
	 - [Read SNM](##Read_SNM)
- [Acknowledgement](##Acknowledgement)
- [Future Works](##Future_works)
----
## Overview
The project is generally focused on the design of 1k*32-bit 6T SRAM memory design.
- SRAM Specification:
	 - Memory Size - 1k*32-bit
	 - Operating voltage - 5V
	 - Technology file - 0.5um SCMOS Technology
---
## Sizing_&_Modes_of_Operations
There are three modes of operations.
- Hold State
- Read Mode
- Write Mode
6T SRAM cell circuit diagram:
![6T SRAM circuit diagram](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/6tsram.jpg)All parameters:
- Vdd=5V
- For NMOS:
	- Vtn =0.496v
	- un =444.9381976 cm^2/Vs
- For PMOS:
	- Vtp = -0.6636V
	- up = 151.3305606 cm^2/Vs
Taken V1=0.49
---
## Read Operations:
Assuming logic 0 is stored in the cell i.e, 
- V1=0V & V2=5V. 
- WL is connected to Vdd.
-  Access transistors(M3,M4)-ON
-  Bitlines Precharged
-  Data stored at node 1 is to be read.

The key design issue for the data-read operation is to guarantee that the voltage V1, does not exceed the threshold voltage of M2 so that the transistor M2 remains turned off during the read phase, i.e., V1 ≤ Vtn. So here the main constraint is V1 ≤ Vtn i.e the strength of M1 should be high than the strength of M3 otherwise data read operation can't be happen. Here M3 operates in **saturation region** and M1 operates in **linear region**.
Here Id3=Id1,so after solving this we get;
![eq-1](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/Eq-1.jpeg)

----
## Write Operation:
Here for the write operations,
-   WL=Vdd
-   Access transistors(M3,M4)-ON
-   BL or BLB=0(According to data-Done by write driver)
-   Whatever data stored at node 1 is to be flipped or written

Assuming logic 1 is stored in the cell i.e, V1=5V & V2=0. WL is connected to Vdd. BL = 0V & BLB = 5V and in data write operation we have to write logic 1 at node 1.
Here the column voltage Vc is forced to logic 0 level by data write circuitry, so Vc is approximately equal to 0V. In order to change the stored information at node 1 i.e V1 to 0V & V2 to Vdd, the node voltage V1 must be reduced below the threshold voltage of M2, so that M2 turns off first. So here the main design constraint is V1 ≤ Vtn (of M2), so that the strength of M3 should be higher than the strength of M5. 

When V1=Vtn, the transistor M3 operates in the **linear region**, M5 operates in **saturation region**.

Here Id3=Id5, after solving this we get,

![eq-2 for write operations](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/Eq-2.jpeg)


So after solving above two equations by putting all the required values we get,

![eq-3 (W5/W3)](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/Eq-3.jpeg)


![eq-4(W3/W1)](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/Eq-4.jpeg)	     

Here 
- **W5**=0.6um, **L5**=0.4um
- **W3**=0.9um, **L3**=0.4um
- **W1**=3um, **L1**=0.4um
---
## Pre-layout
## Dc_Analysis:


	 

   