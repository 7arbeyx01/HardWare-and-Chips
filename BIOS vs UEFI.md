![image](https://github.com/7arbeyx01/HardWare-and-Chips/assets/18347638/6ebed1a9-85ad-4e81-8852-bb7ee5362bd3)

***Firstly, What is Boot Procedure***
1. You press the power button on your laptop/desktop.
2. The CPU starts up, but needs some instructions to work on (remember, the CPU always needs to do something). Since the main memory is empty at this stage, CPU defers to load instructions from the firmware chip on the motherboard and begins executing instructions.
3. The firmware code does a Power On Self Test (POST), initializes the remaining hardware, detects the connected peripherals (mouse, keyboard, pendrive etc.) and checks if all connected devices are healthy. You might remember it as a 'beep' that desktops used to make after POST is successful.
4. Finally, the firmware code cycles through all storage devices and checks the partitioning style (GPT or MBR, If MBR directly loads the boot loader, and if GPT he will go to the protective MBR inside it then loads the boot loader usually located in first sector of a disk). If the boot-loader is found, then the firmware hands over control of the computer to it.
5. So now that the boot-loader is loaded, its job is to load the rest of the operating system. GRUB is one such boot-loader that is capable of loading unix-like operating systems and is also able to chain-load Windows OS. Boot-loader is only available in the first sector of a disk, which is 512 bytes. Given the complexity of modern operating systems, some of these boot-loaders tend to do multi-stage loading, where the main boot-loader loads the second-stage-boot-loader in an environment which is not restricted to 512 bytes.<br>

> Why there is MBR inside GPT?<br>
>The protective MBR is there to ensure that older operating systems or disk management tools that are not aware of GPT won't mistakenly attempt to modify or overwrite the GPT data. Modern systems that support GPT will recognize the GPT header at the beginning of the disk and use that information to understand the partition layout.<br>

***If Unix Based***<br>
6. The boot-loader called ```grub``` then loads the kernel into memory. Unix-like operating systems then run the ```init``` process (the master process, from which other processes are forked/executed) and finally initialize the run-levels. this till **redhat 6**and after redhat 6 initi process has been replaced with systemd and runlevel process replaced with target and there is new process called journald that record logs from the phase of kerenel loading.<br>

***If Windows***<br>
6.The Windows Boot Manager invokes winload.exe —the operating system boot loader—to load the operating system kernel executive (ntoskrnl.exe) and core device drivers. In that respect, wininit.exe is loaded along with some other processes like services.exe for service control, lsass.exe for local security and authority (similar to run-levels) and lsm.exe for local session management, After all this, and after some other drivers are initialized, the Graphical User Inferface (GUI) is loaded and you are presented with the login screen.

## BIOS: Basic Input/Output System. <br>
![image](https://github.com/7arbeyx01/HardWare-and-Chips/assets/18347638/4c899b44-cfcf-4b3a-aedf-ed0537211d13)

It is stored on an EPROM (Erasable Programmable Read-Only Memory), allowing the manufacturer to push out updates easily.

## UEFI: Unified Extensible Firmware Interface. <br>
![image](https://github.com/7arbeyx01/HardWare-and-Chips/assets/18347638/992b0729-f8e6-46e6-83b4-5427c2b1f5aa)

It does the same job as a BIOS, but with one basic difference: it stores all data about initialization and startup in an .efi file, instead of storing it on the firmware.
This .efi file is stored on a special partition called EFI System Partition (ESP) on the hard disk. This ESP partition also contains the bootloader.

***UEFI was designed to overcome many limitations of the old BIOS, including:***

1. UEFI supports drive sizes upto 9 zettabytes, whereas BIOS only supports 2.2 terabytes.
2. UEFI provides faster boot time.
3. UEFI offers security like "Secure Boot", which prevents the computer from booting from unauthorized/unsigned applications. This helps in preventing rootkits, but also hampers dual-booting, as it treats other OS as unsigned applications. Currently, only Windows and Ubuntu are signed OS (let me know if I am wrong).
4. UEFI runs in 32bit or 64bit mode, whereas BIOS runs in 16bit mode. So UEFI  is able to provide a GUI (navigation with mouse) as opposed to BIOS which allows navigation only using the keyboard.

***You might not need UEFI***
 
Though all modern computers come equipped with UEFI by default, some reasons why you might choose BIOS over UEFI are:<br>
1. If you're beginner and don't care about messing with any type of firmware, BIOS is for you.
2. If you have < 2 TB per hard disk or partition, you can go with BIOS.
3. BIOS allows running multiple operating systems without changing any settings This can be a security issue from a modern standpoint, but hey, no hassles for the user.
4. BIOS provides system information to the operating system. So if your OS runs in 16 bit mode, it does not require writing code for interacting with hardware. It can directly use methods provided by BIOS. Else if the OS switches over to 32bit or 64bit mode, then it needs to provide its own subroutines for interacting with hardware.
5. If you are someone who prefers a keyboard and text based UI over navigation with a mouse and GUI, then BIOS is for you.

> UEFI takes these limitations into account and provides a Legacy mode. In it you can run everything as if you had a BIOS firmware. But keep in mind that Intel has announced that it won't support traditional BIOS from 2020.

# Conclusion

# BIOS (Basic Input/Output System):

1. Driver Support:
   - In a traditional BIOS system, drivers for hardware components are often embedded in the system's read-only memory (ROM).
   - This means that the BIOS has built-in support for certain hardware components, and if new hardware is introduced, a BIOS update might be required to add support for it.

2. Firmware Updates:
   - Updating BIOS firmware can be more challenging compared to UEFI. Typically, it involves flashing the BIOS chip with a new firmware version.
   - Flashing BIOS involves a dedicated process and carries some risks, as an interruption during the update can lead to a "bricked" motherboard.

# UEFI (Unified Extensible Firmware Interface):

1. Driver Support:
   - UEFI firmware is more flexible in terms of driver support. Instead of relying on embedded drivers, UEFI can use drivers stored on the system's storage devices.
   - This allows for more modular and extensible driver support. Drivers can be loaded dynamically, and the firmware can support a wider range of hardware without requiring a firmware update.

2. Firmware Updates:
   - UEFI firmware updates are generally more user-friendly. Many UEFI implementations support updating firmware directly from the UEFI environment, often referred to as "in-place" updates.
   - Some UEFI implementations even support updating the firmware from within the operating system, making the process more accessible and less risky than updating traditional BIOS.

***Summary:***
1. BIOS: Embedded drivers, firmware updates typically involve flashing the BIOS chip and carry some risk.
2. UEFI: Modular driver support, firmware updates are often more user-friendly and can be done in-place or from within the operating system.
