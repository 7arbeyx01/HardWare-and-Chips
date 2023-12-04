![image](https://github.com/7arbeyx01/HardWare-and-Chips/assets/18347638/6ebed1a9-85ad-4e81-8852-bb7ee5362bd3)

***Firstly, What is Boot Procedure***
1. You press the power button on your laptop/desktop.
2. The CPU starts up, but needs some instructions to work on (remember, the CPU always needs to do something). Since the main memory is empty at this stage, CPU defers to load instructions from the firmware chip on the motherboard and begins executing instructions.
3. The firmware code does a Power On Self Test (POST), initializes the remaining hardware, detects the connected peripherals (mouse, keyboard, pendrive etc.) and checks if all connected devices are healthy. You might remember it as a 'beep' that desktops used to make after POST is successful.
4. Finally, the firmware code cycles through all storage devices and checks the partitioning style (GPT or MBR, If MBR directly loads the boot loader, and if GPT he will go to the protective MBR inside it then loads the boot loader usually located in first sector of a disk). If the boot-loader is found, then the firmware hands over control of the computer to it.
5. 
## BIOS: Basic Input/Output System. <br>
## UEFI: Unified Extensible Firmware Interface. <br>
