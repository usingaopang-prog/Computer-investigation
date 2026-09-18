# Computer-investigation Report #
Computer investigation with the team 
## Investigation Overview ##
This investigation documents our findings during our testing phase on 14th September . Our Team conducted an inspection of selected computers in the office to identify hardware and performance-related issues. This inspection was conducted to establish a documented baseline and examine the computer performance and issues that may arise from the system in our company. 2. Investigation Structure. The original project is organized into 01-Baseline, 02-CPU, 03-RAM, 04-Storage, 05-Operating-System, 06-Drivers-Updates, 07-Startup, 08-Background-Processes, 09-Applications, 10-Security, 11-Shutdowns, 12-Cooling,13Physical-Hardware, 14-Power-Battery, 15-Network, 16-Workload, 17-Reproduction, 18-Diagnostics, 19 Root-Cause and 20-Recommendation. The supplied evidence directly supports several of these areas and only partially supports others.
## Evidence Register ##
|Evidence |Content captured| Use in investigation|
|---|---|---|
|Photograph 1 |BIOS / Aptio Setup Utility | Baseline, BIOS, CPU, RAM and storageidentification|
|Photograph 2 |Linux lscpu output |CPU architecture, cores, frequency, cacheand virtualisation|
|Photographs 3–6 |htop and stress commands |CPU load, memory use, temperatures,tasks and test results and hardware images|
|Photograph 7| Monitor| We conducted hardware changes |

The photographs contain timestamps and terminal output, with it also showing potential fixes as well.
## Baseline ##
The BIOS screen establishes the main hardware baseline before the Linux operating system is considered. It identifies that each machine is known as Vostro 260 and shows BIOS version A10 with a build date of 22 February 2013. The same screen reports an Intel Core i5-2400 processor, 4096 MB of DDR3 memory at 1333 MHz in dual-channel mode, and a 500.1 GB SATA hard drive. These values provide the reference configuration for the rest of the investigation.
|Component |Recorded information|
|---|---|
|System| Dell Vostro 260|
|BIOS|A10; build date 02/22/2013|
|System date/time shown|14/09/2026; 09:13:41|
|"Service Tag|C4L095J|
|Processor|Intel Core i5-2400 @ 3.10 GHz|
|L2 / L3 cache|1024 KB / 6144 KB|
|Memory|4096 MB DDR3, 1333 MHz, Dual|
|Storage|ST3500413AS (500.1 GB), SATA 0|
|Optical drive|HL-DT-ST DVD+-RW GH70N ATAPI, SATA 1|
|Operating System|Ubuntu 24.04.1 LTS|
|Desktop Environment|GNOME 46|
|Kernel|Linux 6.14.0-35|
|Firmware Version|A10|
## BIOS ##
BIOS evidence is important because it identifies the physical platform and its main installed components independently of the operating system. It also confirms that the 4 GB memory figure and the 500.1 GB drive are not merely values reported by a Linux utility.
<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/60af3c4c-d224-47ed-9414-d87e2a217789" />
