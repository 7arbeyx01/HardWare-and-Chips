![image](https://github.com/7arbeyx01/HardWare-and-Chips/assets/18347638/6ebed1a9-85ad-4e81-8852-bb7ee5362bd3)

***Firstly, What is Boot Procedure***
1. You press the power button on your laptop/desktop.
2. The CPU starts up, but needs some instructions to work on (remember, the CPU always needs to do something). Since the main memory is empty at this stage, CPU defers to load instructions from the firmware chip on the motherboard and begins executing instructions.
3. The firmware code does a Power On Self Test (POST), initializes the remaining hardware, detects the connected peripherals (mouse, keyboard, pendrive etc.) and checks if all connected devices are healthy. You might remember it as a 'beep' that desktops used to make after POST is successful.
4. Finally, the firmware code cycles through all storage devices and checks the partitioning style (GPT or MBR, If MBR directly loads the boot loader, and if GPT he will go to the protective MBR inside it then loads the boot loader usually located in first sector of a disk). If the boot-loader is found, then the firmware hands over control of the computer to it.
5. So now that the boot-loader is loaded, its job is to load the rest of the operating system. GRUB is one such boot-loader that is capable of loading unix-like operating systems and is also able to chain-load Windows OS. Boot-loader is only available in the first sector of a disk, which is 512 bytes. Given the complexity of modern operating systems, some of these boot-loaders tend to do multi-stage loading, where the main boot-loader loads the second-stage-boot-loader in an environment which is not restricted to 512 bytes.
***If Unix Based***
6. The boot-loader called ```grub``` then loads the kernel into memory. Unix-like operating systems then run the ```init``` process (the master process, from which other processes are forked/executed) and finally initialize the run-levels. this till **redhat 6**and after redhat 6 initi process has been replaced with systemd and runlevel process replaced with target and there is new process called journald that record logs from the phase of kerenel loading.
***If Windows***
6.The Windows Boot Manager invokes winload.exe —the operating system boot loader—to load the operating system kernel executive (ntoskrnl.exe) and core device drivers. In that respect, wininit.exe is loaded along with some other processes like services.exe for service control, lsass.exe for local security and authority (similar to run-levels) and lsm.exe for local session management, After all this, and after some other drivers are initialized, the Graphical User Inferface (GUI) is loaded and you are presented with the login screen.

## BIOS: Basic Input/Output System. <br>
## UEFI: Unified Extensible Firmware Interface. <br>
