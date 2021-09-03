# Design and simulation of 6T SRAM
## Table of Contents:

 - [Design of 6T SRAM](#Design_of_6T_SRAM)
 - [Modes of Operations](#Modes_of_Operations)
 - [Pre-layout](#Pre-layout)
	 - [DC Analysis](#DC_Analysis)
	 - [Hold SNM](#Hold_SNM)
	 - [Read SNM](#Read_SNM)
	 - [Sense Amplifier](#Sense_Amplifier)
	 - [Write Driver](#Write_driver)
- [Acknowledgement](#Acknowledgement)
- [Future Works](#Future_works)
- [Contact Information](#Contact_Information)
- ----
## Design_6T_SRAM
The project is generally focused on the design of 1k*32-bit 6T SRAM memory design.
- SRAM Specification: Memory Size - 1k*32-bit, operating voltage 5V, technology file - 0.5um SCMOS Technology
---

Block Diagram:

![blockdiagram](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/block_diagram.jpg)

In this project I have designed and characterised the Bit-cell array that all the devices of SRAM-6T cell using NGSpice tool with 0.5um SCMOS technology.

6T SRAM cell circuit diagram:

![Circuit_diagram](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/circuit%20diagram.jpg)


## Modes_of_Operations
There are three modes of operations.
- Hold State
- Read Mode
- Write Mode

All parameters:
- Vdd=5V
- For NMOS: Vtn =0.496v, un =444.9381976 cm^2/Vs
- For PMOS: Vtp = -0.6636V, up = 151.3305606 cm^2/Vs
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


So after solving above two equations by putting all the required values we get, w5/w3<0.66 and w3/w1<0.26.	     

Here 
- **W5**=0.6um, **L5**=0.4um
- **W3**=1um, **L3**=0.4um
- **W1**=4um, **L1**=0.4um
---
## Pre-layout
## DC_Analysis:

From the VTC we can get the operating point of the CMOS Inverters. Here it is 1.12V.

## Hold_SNM


![Hold_SNM](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/SNM_Hold.jpg)



![snm_hold_graph](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/snm_hold_graph.jpg)

	 
	 
## Read_SNM


![SNM_READ](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/SNM_Read.jpg)



![snm_read](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/snm_read_graph.jpg)

   

---
### Circuit Diagram of SRAM Cell with all Parasitics


![SRAM_PARASITICS](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/sram_parasitics.jpg)


In the above circuit diagram consists of SRAM_6T cell with all its parasitics, precharged circuit, sense amplifier and write driver.As 1kx32-bit SRAM consists of 32k of bit cells, so it can taken as 128*256 number of cells(i.e. 128 number of rows and 256 number of columns). For Simulation we are taking one 6T SRAM cell with the parasitic capacitor of all the cells. cw1, cw2, cw3 are the wire load capacitors(10fF/cell) which are connected to BIT, complementary BIT and word line. Simillarly M6, M7, M8, M9 are the parasitic mosfets which is equaly do the operation like 1kx32-bit cell array. Here I have done a Transiant analysis(excluding sense Amp and write driver).

### Transient Analysis


![tran_parasitics](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/tran_precharge.jpg)



## Sense_Amplifier
Sense Amplifier generally used to detect the node voltage stored in the memory. It will be operate at the time of Read operation. I have used a latch based Sense amplifier in my design.



![sense_amp](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/sense_amp.jpg)


### Simulation result of 6T SRAM cell with Sense Amplifier

![tran_sense_amp](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/tran_sense_amp.jpg)



## Write_Driver

The write drivers send the input data signals onto the bit-lines for a write operation. The write drivers are tri-stated so that they can be placed between the column multiplexer/memory array and the sense amplifiers. There is one write driver for each input data bit.


![Write_driver](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/write_driver.jpg)


### Simulation result of 6T SRAM cell with Sense Amplifier and Write Driver


![tran_SA_WD](https://github.com/Bijayalaxmi9/6T_SRAM/blob/main/Images/tran_SA_WD.jpg)



## Acknowledgement

-   Dr.Saroj Rout,Associate Professor,Silicon Institute Of Technology,Bhubaneswar
-   Mr.Santunu Sarangi,Assistant Professor,Silicon Institute Of Technology,Bhubaneswar
- ---
## Future_Works
- To create the layout using Magic.
-   To do post layout simulation.
- ---
## Contact_Information
-   Bijayalaxmi Sahoo, Design Engineer,  [Sevya Multimedia Technologies Pvt. Ltd.](https://sevyamultimedia.com/)
-   [bijayalaxmisahoo100@gmail.com](mailto:bijayalaxmisahoo100@gmail.com)
