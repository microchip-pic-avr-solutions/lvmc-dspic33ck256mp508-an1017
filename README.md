![image](images/microchip.jpg) 

# LVMC DSPIC33CK256MP508 AN1017

## INTRODUCTION
<p style='text-align: justify;'>
This demonstration describes a method of driving a hall sensor based Permanent Magnet Synchronous Motor (PMSM) with sinusoidal applied voltage controlled by dsPIC33CK256MP508 Digital Signal Controller (DSC). 
The demonstration code uses 3 hall sensors from the motor to know the 6 states commutation within 1 electrical cycle and interpolates the angles in between the 6 states to generate a continuous angle needed for sinusoidal voltage.</p>

## APPLICATION FEATURES
- <p style='text-align: justify;'>Sinusoidal current generation for controlling PMSM motor phases using Space Vector Modulation (SVM)</p>
- <p style='text-align: justify;'>Synchronization of sinusoidal voltages to PMSM motor position</p>
- <p style='text-align: justify;'>Closed-loop speed regulation using digital Proportional Integral Derivative (PID) control</p>
- <p style='text-align: justify;'>Phase advance operation for increased speed range</p>
- <p style='text-align: justify;'>Fractional math operations performed by the DSP engine of the dsPIC® DSC</p>


## SENSORED OPERATION OF BLDC MOTORS

<p style='text-align: justify;'>To allow correct commutation of the motor, the absolute position within an electrical cycle must be measured. Three Hall effect sensors provide rotor position information. These sensors are distributed along the stator in such a way that they generate six different logic states per electrical cycle. The ratio between the electrical cycles and mechanical revolutions depends on the number of motor pole pairs. 
For instance, the motor used in this application note has five pole pairs, so every mechanical revolution requires five electrical cycles. 
For conventional energization (six-step commutation), six equally spaced commutations are required per electrical cycle. 
This is usually implemented using three Hall effect or optical switches with a suitable disk on the rotor.Continuous position information is not required. 
Only detection of the required commutation instances is required.
Figure 1 shows the three sensor outputs along with the corresponding voltage driving each motor winding.</p>

 <p align="center">
  <img  src="images/Figure1.png"></p>
 <p align = "center"> Figure 1  six-step commutation for trapezoidal BLDC motors
</p> 
<br />

<p style='text-align: justify;'>You can see that the voltage does not vary for each particular sector until a new motor position or combination of Hall effect sensor is detected. For the technique described in this application note, the three Hall effect sensors detect the rotor position, as in the six-step technique. However, instead of generating square waves, a continuous changing voltage is generated with a sine-wave shape. Figure 2 shows the resulting sinusoidal voltage generation. The relation is shown between the phase voltages and the three Hall effect sensors. The amplitude of the sinusoidal voltages determines the speed 
for a specific mechanical load in the motor.</p>

 <p align="center">
  <img  src="images/Figure2.png"></p>
  <p align = "center">Figure 2 voltage generation for Sinusoidal BLDC motors
</p>
  

## Hardware Connection and Running the Demo Code

## Suggested Demonstration Requirements
Motor Control Application Firmware Required for the Demonstration
- <https://bitbucket.microchip.com/projects/MCU16CE/repos/lvmc-dspic33ck256mp508-an1017>
> **_NOTE:_**
> In this document, hereinafter this firmware package is referred as firmware.
## Software Tools Used for Testing the firmware
- MPLAB® X IDE v5.50 or later
- MPLAB® XC16 Compiler v1.70
- MPLAB® X IDE Plugin: X2C-Scope v1.30 or later
> **_NOTE:_**
>The software used for testing the firmware prior to release is listed above. It is recommended to use the version listed above or later versions for building the firmware.
## Hardware Tools Required for the Demonstration
- dsPIC33CK Low Voltage Motor Control Board, Part-No. [DM330031](https://www.microchip.com/developmenttools/ProductDetails/PartNO/DM330031)
- 24V Power Supply, Part-No. [AC002013](https://www.microchipdirect.com/dev-tools/AC002013)
- 24V 3-Phase Brushless DC Motor, Part-No. [AC300020](https://www.microchip.com/en-us/development-tool/AC300020)  <br />
> **_NOTE:_**
> All items listed under the section Hardware Tools Required for the Demonstration are available at [microchip DIRECT](https://www.microchipdirect.com/)

## Hadware Setup
<p style='text-align: justify;'>This section describes hardware setup required for the demonstration. Motor terminals connections and hall effect sensor connections are described here.</p>

<p style='text-align: justify;'>
1. Connect the three phase wires from the motor to PHA, PHB & PHC terminals of connector J14, provided on the Development Board as mentioned in the below table.</p> 


| LVMC Board|Hurst075 Motor| |
| :--------:| :-----------:|:--:|
|           |Winding Terminals (Color as per image below) | Molex 39-01-2040(Mating Connector)    |
| PHC   | Red   | 1|
| PHB   | Black | 2|
| PHA   | White | 3|

<br />
<p style='text-align: justify;'>
2. Connect the hall sensors from the motor to HA, HB and HC terminals of connector J7, provided on the Development Board as mentioned in the below table. </p>

|MCLV2 Board|	Hurst075 Motor||
|:---:|:----------------------:|:----------------------:|
||Hall Terminals(Color as per image above)|	Molex 50-57-9408 (Mating Connector)|
|5V|	Red|	1|
|GND|	Black|	2|
|HA	| White	|4|
|HB	|Brown|	3|
|HC|	Green|	5|

<br />
<p align="center">
  <img  src="images/LVMC_Sensored Connection diagram.png"></p>
 <p align = "center"><font size="2"> Figure 3  LVMC Sensored Connection diagram
</p> 
<p style='text-align: justify;'>
3.	Plug in the 24V power supply to connector J1 or J2 provided on the dsPIC33CK Low Voltage Motor Control Board.</p>
<br />
<p align="center">
  <img  src="images/LVMC_Power Supply Connector.png"></p>
 <p align = "center"><font size="2"> Figure 4  LVMC Power Supply Connector
</p> 
<p style='text-align: justify;'>
4.	The board has an on-board programmer ‘PICKIT™ On Board (PKOBv4)”, which can be used for programming or debugging dsPIC33CK256MP508 device. To use on-board programmer, connect a micro USB cable between Host PC and Connector J13 provided on the dsPIC33CK Low Voltage Motor Control Board.</p>
<p align="center">
  <img  src="images/LVMC_PKOB4.png"></p>
 <p align = "center"><font size="2"> Figure 5  LVMC PKOB4
</p> 
<p style='text-align: justify;'>
5.	Alternatively, connect the Microchip programmer/debugger MPLAB PICkit 4 In-Circuit De-bugger to the Connector J10 of the dsPIC33CK Low Voltage Motor Control Board as shown below and to the Host PC used for programming the device. Ensure that PICkit 4 is connected in correct orientation.</p>

<p align="center">
  <img  src="images/LVMC_Programming Connector.png"></p>
 <p align = "center"><font size="2"> Figure 6  LVMC Programming Connector
</p> 
<br />

## SOFTWARE SETUP AND RUN
### Setup: MPLAB X IDE and MPLAB XC16 Compiler
<p style='text-align: justify;'>
Install MPLAB X IDE and MPLAB XC16 Compiler versions that support the device dsPIC33CK256MP508 and PKOBv4. The version of the MPLAB X IDE, MPLAB XC16 Compiler and X2C-Scope plug-in used for testing the firmware are mentioned in the section Software Tools Used for Testing the firmware. To get help on </p>

- MPLAB X IDE installation, refer [link](https://microchipdeveloper.com/mplabx:installation)
- MPLAB XC16 Compiler installation steps, refer [link](https://microchipdeveloper.com/xc16:installation)

<p style='text-align: justify;'>If MPLAB IDE v8 or earlier is already installed on your computer, then run the MPLAB driver switcher (It is installed when MPLAB®X IDE is installed) to switch from MPLAB IDE v8 drivers to MPLAB X IDE drivers. If you have Windows 7 or 8, you must run MPLAB driver switcher in ‘Administrator Mode’. To run the Device Driver Switcher GUI application as administrator, right click on the executable (or desktop icon) and select ‘Run as Administrator’. For additional details refer MPLAB X IDE help topic “Before You Begin: Install the USB Device Drivers (For Hardware Tools): USB Driver Installation for Windows Operating Systems”. </p>

### Setup: X2C - SCOPE
<p style='text-align: justify;'>
X2C - SCOPE is a MPLAB X IDE plugin that allows a developer to interact with an application while the application program is running. X2C-Scope enables you to read, write, and plot global variables (for motor control) in real time. It communicates with the target using the UART. To use X2C, the plugin must be installed:</p>

- In MPLAB X IDE, select Tools>Plugins and click on the Available Plugins tab.
- Select X2C - SCOPE plug-in by checking its check box, and then click Install.
- Look for tool X2C - SCOPE under Tools>Embedded.

<p align="center">
  <img  src="images/X2C Scope Configuration.png"></p>
 <p align = "center"><font size="2"> Figure 7  X2C Scope Configuration
</p> 
<br />

##  BASIC DEMONSTRATION
### Firmware Description
<p style='text-align: justify;'>
The firmware version required for the demonstration is mentioned under the section Motor Control Application Firmware Required for the Demonstration.</p>
<p style='text-align: justify;'>
This firmware is implemented to work on Microchip’s 16-bit Digital signal controller (dsPIC® DSC) dsPIC33CK256MP508. 
For more information, see the dsPIC33CK256MP508 Family datasheet (DS70005349).</p>
<p style='text-align: justify;'>
The Motor Control Demo application uses push button to start or stop the motor and poten-tiometer to vary speed of the motor.</p>
<p style='text-align: justify;'>
For more details refer Microchip Application note AN1017 “Sinusoidal Control of PMSM Motors with dsPIC30F / dsPIC33F/ dsPIC33E DSC” available at Microchip web site </p>

> **_NOTE:_**
> The project may not build correctly in Windows OS if Maximum path length of any source file in the project is more than 260 characters. In case absolute path is exceeding or nearing maximum length, do any (or both) of the following:
 > - Shorten the name of the directory containing the firmware used in this demonstration. In this case, rename directory AN1017_dsPIC33CK256MP508_LVMC to more ap-propriate shorter name. In case you renamed the directory, consider the new name while reading instructions provided in the upcoming sections of the document. 
> - Place firmware in a location, such that absolute path length of each file included in the projects does not exceed the Maximum Path length specified. 
For details, refer MPLAB X IDE help topic “Path, File and Folder Name Restrictions”.

### Basic Demonstration
<p style='text-align: justify;'>
Follow below instructions step by step to setup and run the motor control demo application:</p>

1. <p style='text-align: justify;'> Start MPLAB X IDE and open (File>Open Project) the project bldc.X with device selection dsPIC33CK256MP508.</p>
<p align="center">
  <img  src="images/IDE_Device selection.png"></p>
 <p align = "center"><font size="2"> Figure 8  IDE Device selection
</p> 

2. <p style='text-align: justify;'>Set the project bldc.X as main project by right clicking on the project name and selecting “Set as Main Project” as shown. The project “bldc” will then appear in bold.</p>
 <p align="center">
  <img  src="images/IDE_Project setup.png"></p>
 <p align = "center"><font size="2"> Figure 9  IDE Project setup
</p> 
	
3. <p style='text-align: justify;'>	Open bldc_main.h (under bldc.X -> headerfiles) in the project bldc.X & define the OPENLOOP for Open Loop running & Undefine it for closed loop operation </p>
  <p align="center">
  <img  src="images/Project_Open loop set up.png"></p>
 <p align = "center"><font size="2"> Figure 10  Open loop set up
</p> 

4. <p style='text-align: justify;'>Comment out the #define PHASE_ADVANCE for above base speed applications </p>
  <p align="center">
  <img  src="images/Project_Phase advance set up.png"></p>
 <p align = "center"><font size="2"> Figure 11  Phase advance set up
</p>

5. <p style='text-align: justify;'>Right click on the project bldc.X and select “Properties” to open its Project Properties Dialog. Click the “Conf: [default]” category to reveal the general project configuration information.</p>

    In the ‘Conf: [default]’ category window: 
    - Select the specific Compiler Toolchain from the available list of compilers. Please ensure MPLAB® XC16 Compiler supports the device dsPIC33CK256MP508. In this case “XC16(v1.70)” is selected. The compiler used for testing the firmware is listed in the section Software Tools Used for Testing the firmware.
    - Select the Hardware Tool to be used for programming and debugging. In this case, “MPLAB PKoB 4” is the selected programmer.
    - After selecting Hardware Tool and Compiler Toolchain, click button Apply
 
        <p align="center">
        <img  src="images/Project_Properties settings.png"></p>
        <p align = "center"><font size="2"> Figure 12  Project Properties settings
        </p>

6. <p style='text-align: justify;'>	To build the project (in this case bldc.X) and program the device dsPIC33CK256MP508, click “Make and Program Device Main project” on the toolbar.</p>

  <p align="center">
  <img  src="images/Device_Programming.png"></p>
 <p align = "center"><font size="2"> Figure 13  Device Programming
</p>
  
7. <p style='text-align: justify;'>		If the device is successfully programmed, LD10 (‘LED2) will be turned ON, indicating that the dsPIC® DSC is enabled.</p> 

8. <p style='text-align: justify;'>		Run or Stop the motor by pressing the push button SW1. The function of the pushbutton SW1 (Run/Stop of the motor) is indicated by turning ON or OFF the LED1 (LD11).</p>

  <p align="center">
  <img  src="images/Push buttons.png"></p>
 <p align = "center"><font size="2"> Figure 14  Push buttons
</p>
 
9. <p style='text-align: justify;'>	If desired, the motor speed can be varied using the potentiometer (labeled “POT1”).</p>

  <p align="center">
  <img  src="images/Potentiometer.png"></p>
 <p align = "center"><font size="2"> Figure 15  Potentiometer
</p>
 
10.	<p style='text-align: justify;'>To reverse the direction of rotation, press the push button SW2.</p>
11.	<p style='text-align: justify;'>Press the push button SW1 to stop the motor.</p>

> **_NOTE:_**
>The macro definitions MAX_MOTORSPEED, MAX_MOTORCURRENT, POLEPAIRS, SECTOR and MAX_BOARDCURRENT are specified in bldc_main.h file included in the project bldc.X. The definitions MAX_MOTORSPEED and MAX_MOTORCURRENT are defined as per the specification provided by the Motor manufacturer. Exceeding manufacturer specification may lead to damage to the motor or (and) the board. 

## Data visualization through X2CScope Plug-in of MPLABX
<p style='text-align: justify;'>
The application firmware comes with initialization required to interface Controller with Host PC to enable Data visualization through X2C Scope plug-in. X2C-Scope is a third-party plugin for MPLAB X which facilitates real-time diagnostics.</p>

1. Ensure X2C Scope Plug-in is installed. For additional information on how to set up a plug-in refer https://microchipdeveloper.com/mplabx:tools-plugins-available

2. <p style='text-align: justify;'>To utilize X2C communication for this demonstration, a micro-USB connection is required between Host PC and dsPIC33CK Low Voltage Motor Control Board. PKob 4 Connector J13 can be used to communicate between Host PC and dsPIC33CK Low Voltage Motor Control Board, alternatively Connect a micro-USB cable from your computer to the J6 connector of the dsPIC33CK Low Voltage Motor Control Board.</p>

 <p align="center">
  <img  src="images/X2C_Interface.png"></p>
 <p align = "center"><font size="2"> Figure 16  X2C Interface
</p>

3.	<p style='text-align: justify;'>Ensure application is configured and running as described under Section Basic Demonstration by following steps 1 through 11.</p>

4.	<p style='text-align: justify;'>Build the project bldc.X. To do that right click on the project bldc.X and select “Clean and Build”.</p>

 <p align="center">
  <img  src="images/Project_Clean&Build.png"></p>
 <p align = "center"><font size="2"> Figure 17  Clean and Build
</p>
 
5.	<p style='text-align: justify;'>Please ensure that the checkbox “Load symbols when programming or building for pro-duction (slows process)” is checked, which is under the “Loading” category of the Project Properties window</p>

 <p align="center">
  <img  src="images/Load Variables.png"></p>
 <p align = "center"><font size="2"> Figure 18  Load Variables
</p>

6.	<p style='text-align: justify;'>To build the project (in this case bldc.X) and program the device dsPIC33CK256MP508, click “Make and Program Device Main project” on the toolbar.</p>

 <p align="center">
  <img  src="images/Device_Programming.png"></p>
 <p align = "center"><font size="2"> Figure 19  Device Programming
</p>

7.	<p style='text-align: justify;'>Open the X2C window by selecting Tools>Embedded>X2CScope.</p>

 <p align="center">
  <img  src="images/X2C Selection.png"></p>
 <p align = "center"><font size="2"> Figure 20  X2C Selection
</p>

8.	<p style='text-align: justify;'>Open the X2CScope Configuration window and in “Select project” menu, select bldc project as shown.</p>

 <p align="center">
  <img  src="images/X2C Project selection.png"></p>
 <p align = "center"><font size="2"> Figure 21  X2C Project selection
</p>

9.	<p style='text-align: justify;'>Remote Communication needs to be established, as indicated in the following figure. Ensure the communication baud rate is set to 115200 as the same is set in the application firmware, while COM port used depends on the system settings. Refresh button lists the available COM Ports. Select the COM Port as per the connection.</p>
 <p align="center">
  <img  src="images/X2C Connection setup.png"></p>
 <p align = "center"><font size="2"> Figure 22  X2C Connection setup
</p>


10.	<p style='text-align: justify;'>Once COM port detected, click on “Disconnected”, and it will be turn into “Connected”, if the link is established as programmed.</p>
  <p align="center">
  <img  src="images/X2C Connection Button.png"></p>
 <p align = "center"><font size="2"> Figure 23  X2C Connection Button
</p>

11.	<p style='text-align: justify;'>Set the “Project Setup” as shown below and click “Set Values”. Set Scope sample time as interval at which X2CScopeUpdate() is called. In this application it is every 20kHz (50µs).</p>
 <p align="center">
  <img  src="images/X2C Project Setup.png"></p>
 <p align = "center"><font size="2"> Figure 24  X2C Project Setup
</p>


12.	<p style='text-align: justify;'>When the setup is established, click on open scope View (under sub window “Data Views”), this open Scope Window.</p>

 <p align="center">
  <img  src="images/X2C Dataview.png"></p>
 <p align = "center"><font size="2"> Figure 25  X2C Dataview
</p>    	     

13.	<p style='text-align: justify;'>In this window, select the variables that needs to be monitored. To do this, click on the source against each channel, a window Select Variables opens upon the screen. From the available list, the required variable can be chosen. Ensure check boxes Enable & Visible are checked for the variables to be plotted.</p>

    To view data plots continuously, uncheck Single-shot. When Single-shot is checked it captures the data once and stops. The Sample time factor value multiplied with Sample time determines the time difference between any two consecutive data points on the plot.

 <p align="center">
  <img  src="images/X2C Datapoint selection.png"></p>
 <p align = "center"><font size="2"> Figure 26  X2C Datapoint selection
</p>
 

14.	<p style='text-align: justify;'>Click on SAMPLE, then X2C scope window shows variables in real time, which is updated automatically.</p>
  <p align="center">
  <img  src="images/X2C Sample.png"></p>
 <p align = "center"><font size="2"> Figure 27  X2C Sample
</p>


15.	<p style='text-align: justify;'>Click on ABORT to stop.</p>

 <p align="center">
  <img  src="images/X2C Abort.png"></p>
 <p align = "center"><font size="2"> Figure 28  X2C Abort
</p>

  
## REFERENCES:
For additional information, refer following documents or links.
1.	AN1017 Application Note “Sinusoidal Control of PMSM Motors with dsPIC30F / dsPIC33F/ dsPIC33E DSC”
2.	AN957 Application Note “Sensored BLDC Motor Control Using dsPIC30F2010”
3.	dsPIC33CK Low-Voltage Motor Control Development Board (DM330031) User's Guide 
4.	dsPIC33CK256MP508 Family datasheet (DS70005349).
5.	Family Reference manuals (FRM) of dsPIC33CK256MP508 family
6.	MPLAB® X IDE User’s Guide (DS50002027) or MPLAB® X IDE help 
7.	MPLAB® X IDE installation
8.	MPLAB® XC16 Compiler installation





