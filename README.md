# Smart-Sign-Language-Translation-Gloves
Intelligent translation of sign language for simple interaction between deaf and dumb people


<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
- [Introduction](#introduction)
    - [Function](#function)
    - [System Architecture](#system-architecture)
- [Hardware and Software Setup](#hardware-and-software-setup)
    - [Required Hardware](#required-hardware)
    - [Required Software](#required-software)
    - [Hardware Connection](#hardware-connection)
- [User Manual](#user-manual)
    - [Before Running This Application](#before-running-this-application)
    - [Run This Application](#run-this-application)
 <!-- markdown-toc end -->

# Introduction
This glove is designed to facilitate communication between deaf and dumb people.
## Function
   - **Chinese mode**<br/>
     The gloves read out the corresponding **Chinese by recognizing sign language gestures**.
     
      ![image](https://github.com/mk997630105/Smart-Sign-Language-Translation-Gloves/blob/master/hello3.gif)
   - **English mode**<br/>
     The gloves read out the corresponding **English alphabet by recognizing sign language gestures**.
     
      ![image](https://github.com/mk997630105/Smart-Sign-Language-Translation-Gloves/blob/master/C(4).gif)
   - **Auto play mode**<br/>
     The gloves read out the **user-defined common language** by recognizing sign language gestures.
   - **Speech Recognition**<br/>
     The gloves can **identify some commonly used words* in life to users.
     
     ![image](https://github.com/mk997630105/Smart-Sign-Language-Translation-Gloves/blob/master/age.gif)
   - **Danger warning**<br/>
     The gloves can alert the user to the vehicle by recognizing the sound of the horn.
     
      ![image](https://github.com/mk997630105/Smart-Sign-Language-Translation-Gloves/blob/master/clump12.gif)
   - **One-click assistance**<br/>
     When in trouble, users can send their location information to their families for help.
     
      ![image](https://github.com/mk997630105/Smart-Sign-Language-Translation-Gloves/blob/master/one.gif)
## System Architecture
   ![image](https://github.com/mk997630105/Smart-Sign-Language-Translation-Gloves/blob/master/structure.PNG)
# Hardware and Software Setup
## Required Hardware   
   - 1 DesignWare ARC EM Starter Kit(EMSK)
   - 1 Acceleration sensor(JY-901)
   - 1 Speech recognition module(SYN6288)
   - 1 AD converter(PmodAD2)
   - 1 OLED display module(SSD1306)
   - 1 Speech recognition module(YS-LDV7)
   - 1 GPS(C3-470A)
   - 1 GPRS(SIM900A)
   - 1 SD Card
   
## Required Software
   - Metaware or ARC GNU Toolset
   - Serial port terminal, such as putty, tera-term or minicom

## Hardware Connection
   1. The EMSK implement smart gloves,it will processe the data collected by sensors and translate gestures to corresponding sign language, we can get the corresponding sign language information by displaying text and making voice.
      - Connect JY-901 to J1(Using UART interface)
      - Connect SYN6288,PmodAD2 and SIM900A to J4(Using I2C interface)
      - Connect C3-470A to J5(Using UART interface)
      - Connect SSD1306 to J2(Using I2C interface)
      - Connect YS-LDV7 to J3
   2. Configure your EMSKs with proper core configuration
   - EMSK connection
   ![image](https://github.com/mk997630105/Smart-Sign-Language-Translation-Gloves/blob/master/picture/connection.jpg)
   
# User Manual
## Before Running This Application
  Download source code of Master Sign Language from github.
  - The hardware resources are allocated as following table.
  
| Hardware Resource  | Functioon                      |
| ------------------ | -----------------------------  |
| JY-901             | Acceleration and angle sensor  |
| Flex2.2            | Flex sensor                    |
| SYN6288            | Voice composite                |
| C3-470A            | position                       |
| SIM900A            | send messages                  |
  
## Run This Application
  Here take EMSK2.0 - ARC EM7D with GNU Toolset for example to show how to run this application.We need to use embARC bootloader to automatically load application binary for different EMSK and run. See embARC Secondary Bootloader Example for reference.
### Makefile
   - Target options about EMSK and toolchain

```
         BOARD ?= emsk
         BD_VER ?= 20
         CUR_CORE ?= arcem7d
         TOOLCHAIN ?= gnu
```
   - The relative series of the root directory, here the path of the Makefile is .\embARC\example\emsk\sign language/makefile:
```
         #
         # root dir of embARC
         #
         EMBARC_ROOT = ../../..
         MID_SEL = common u8glib
```  
  See embARC Example User Guide, "Options to Hard-Code in the Application Makefile" for more detailed information about Makefile Options
  
  - Driver<br/>
  Placing the drivers' source code in driver folder, you can see there are subfolders for data,judge,draw and gprs drivers. Placing the C source file and header file in the corresponding subfolder.

| folder/file      | Function                                           |
| ---------------- | -------------------------------------------------  |
| data             | get and deal with data from sensor                 |
| draw             | OLED driver                                        |
| gprs             | send position information                          |
| judge            | match the collected data with the sample database  |
