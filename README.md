# Computer-investigation Report #
Hardware, Performance and Stress-Test Investigation

*Team: Felicity, Tshifhiwa, Mahlatsi, Opang  and Kyle*

## Investigation Overview ##
This investigation documents our findings during our testing phase on 14th September . Our Team conducted an inspection of selected computers in the office to identify hardware and performance-related issues. This inspection was conducted to establish a documented baseline and examine the computer performance and issues that may arise from the system in our company. 2. Investigation Structure. The original project is organized into Baseline ,BIOS ,CPU ,RAM ,Operating System ,Background ,Processes Network ,Investigation ,Cooling ,Workload ,Monitor ,Reproduction ,Diagnostics ,Storage and SMART diagnostics, Physical Hardware and Network,Startup Performance,Security Audit ,Root Cause ,Recommendations ,Overall Findings, ,Commands used,Tags and Code. The supplied evidence directly supports several of these areas and only partially supports others.

## Evidence Register ##

|Evidence |Content captured| 
|---|---|
|Photograph 1 |BIOS Setup Utility | 
|Photograph 2 |Linux lscpu output |
|Photograph 3|Htop and stress commands |
|Photograph 4|Smartctl drive identification and SMART health result|
|Photograph 5| SMART self-test history and systemd-analyze timing|
|Photograph 6| Stress test|
|Photograph 7| Monitor purple display|
|Photograph 8| Monitor with clear display|
|Photograph 9| Smartctl drive identification and SMART health result|
|Photograph 10| Startup |
|Photograph 11| Lynis package, service and system-hardening suggestions|
|Photograph 12| Lynis boot, authentication and filesystem suggestions |
|Photograph 13| Lynis network, printing, logging and banner suggestions |
|Photograph 14| Lynis audit, file-integrity, permissions, kernel and malware-scanning suggestions|

*The photographs contain timestamps and terminal output, with it also showing potential fixes as well.*

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
## CPU ##
We use command lscpu to confirm that we have a 64-bit x86 system that uses an Intel Core i5-2400. Four logical CPUs are online, matching the four physical cores shown in the output, with one thread per core and one socket. The processor is reported with a maximum frequency of 3400 MHz and a minimum of 1600 MHz. VT-x virtualization is also present. Cache information shown by lscpu includes 128 KiB L1 data cache, 128 KiB L1 instruction cache, 1 MiB L2 cache and 6 MiB L3 cache. The data shows a functioning four-core processor with normal frequency scaling available between the reported minimum and maximum values.
|CPU characteristic|Value|
|---|---|
|Architecture|x86_64|
|CPUs / cores|4/4|
|Threads per core|1|
|Socket|1
|Frequency range|1600–3400 MHz|
|Virtualization|VT-x|
|Cache|L1d 128 KiB; L1i 128 KiB; L2 1 MiB; L3 6 MiB|
<img width="533" height="583" alt="image" src="https://github.com/user-attachments/assets/bf0b3953-fab9-4aa2-89eb-20f97bc2aa12" />

## RAM ##
The BIOS records 4096 MB of DDR3 memory running at 1333 MHz in dual-channel mode. During htop monitoring, approximately 3.74 GB of memory was shown as available to the operating system, with observed memory use around 1.0–1.8 GB in the captured sessions. Swap remained at 0 KB of 3.74 GB in the displayed monitor. IT using 40-43 % of RAM without any applications open shows that we need to have a change of RAM. With the figure below showing us that 1 Ram stick is 2 GB and takes all the RAM slots which is not enough for the system.Due to the slow nature of the RAM applications were hard to test as they slow and unresponsive and struggled to multitask.
<img width="583" height="402" alt="image" src="https://github.com/user-attachments/assets/630af961-a0b6-4f29-8373-8187a3469066" />

## Operating System ##
The system is running Ubuntu 24.04.1 LTS. The captured software environment reports GNOME version 46 and Linux kernel version 6.14.0-35. The BIOS and firmware version are both recorded as A10. There are no issues with the operating system and no reported changes

## Background Processes ##
The htop photographs show a normal desktop process environment with roughly 121–149 tasks visible and approximately 99 threads. Processes and services including systems, avail, message bus, toolkit and GNOME-related components are visible in the list. CPU percentages for individual background processes are generally small in the captured views. With how small our RAM is these small processes do consume 40% of Ram but only due to our

## Network Investigation ##
Our network speed test recorded 44.28 Mb/s download and 2.41 Mb/s upload. Our test server was in London servers and the observed latency was approximately 1028.6 ms.The routing output shows enp2s0, source/local address 192.168.0.69/24 and default route 192.168.0.1. Records in our screenshot show computers failed in address-command attempts; the successful route output provides the interface and source address.

|Measurement| Observed result|
|---|---|
|Download|44.28 Mb/s|
|Upload|2.41 Mb/s|
|Latency|1028.6 ms to selected London server|
|Interface|enp2s0|
|Local IPv4|192.168.0.69/24|
|Default gateway|192.168.0.1|

<img width="1280" height="575" alt="image" src="https://github.com/user-attachments/assets/71c663ef-4da6-4e23-b33f-f1e626c8b607" />


## Cooling ##
We used htop to find the ranges which are approximately 51°C to 58°C across the displayed CPU cores during load. The highest value is about 58°C. At the same time, CPU utilization was shown at or near full load.

<img width="557" height="587" alt="image" src="https://github.com/user-attachments/assets/27d64027-115f-4bc9-a510-f3f1484e47e7" />

## Workload ##
The workload increased using the Linux stress utility while htop was used to observe system activity. The captured commands include a four-CPU stress workload for 60 seconds, a virtual-memory workload using two workers and 256 MB each for 30 seconds, and a CPU/I/O workload using two CPU workers and two I/O workers for 45 seconds. These tests were designed to place controlled demand on the processor, memory and I/O path.

|Test|Observed configuration|Observed result|
|---|---|---|
|CPU stress|4 CPU workers; 60 seconds|Completed successfully|
|Memory stress|2 VM workers; 256 MB; 30 seconds|Completed successfully|
|CPU + I/O stress|2 CPU + 2 I/O workers; 45 seconds|Completed successfully|
<img width="552" height="573" alt="image" src="https://github.com/user-attachments/assets/90019218-c2dd-48a5-99b1-e9ae3848bf29" />

## Monitor ##
We had a monitor that had and colour issue, it was unable to display properly, even when we put in on factory default it reminds to have this purple colour the issue is related to the cable responsible for transmitting the video signal from the computer to the display. We found that the issue was with the VGA cable and replacing the cable with HDMI made the monitor have colour. I would say monitor sizes are optimal and can give bad results when making something due to difference in the resolutions for certain applications and sites.
<img width="743" height="414" alt="image" src="https://github.com/user-attachments/assets/01fe5319-fbfc-4a32-b077-20d1bb88cde2" />

<img width="1600" height="719" alt="image" src="https://github.com/user-attachments/assets/ca8d2a99-30e7-47ed-b33b-d9f1c57d121b" />

## Reproduction ##
The stress tests provide a controlled reproduction environment for high CPU and memory demand. During the runs, the computer continued to display htop information while the stress commands ran, and the terminal reported successful completion. No crash forced shutdown or visible lock-up is shown in the supplied evidence. While for the monitor, we were able to make the display purple again and determine that the cabling was the issue.

## Diagnostics ##
Three main tools are visible in the evidence. The lscpu utility identifies the processor, topology, frequency limits, cache and virtualization support. htop provides live process, CPU, memory and temperature monitoring. The stress utility applies controlled workloads and reports when those workloads finish. Together, these tools provide both static
configuration evidence and dynamic performance evidence.

## Storage and SMART diagnostics ##
We use the new smartctl -a /dev/sda to identify we posses a Seagate Barracuda 7200.12, model ST3500418AS, 500 GB, 512-byte logical/physical sectors, 7200 RPM and SATA 2.6 / 3.0 Gb/s capability. SMART diagnostics gave us an overall health assessment that deemed that the drive has passed.Our own observations has deemed slow boot times are caused by our HDD, as our OS is saved there. And it is known that HDD is not a good standard for fast booting
<img width="2048" height="1536" alt="image" src="https://github.com/user-attachments/assets/bbf107ee-8f77-437c-9210-d748440913d6" />

## Physical Hardware and Network ##
Photograph 3 shows the internal of the system, there is 2 Ram stick, network card, Battery and CPU. The issue seems is thermal paste looks almost done and seemly old on the CPUs. The Ram is 2 2GB of RAM which is too small for system. 

## Startup Performance ##
We utilised systemd-analyze in the kernel which recorded 5.398 s kernel + 1 min 19.722 s userspace = 1 min 25.121 s in total. These statics provide use a concrete measurement for our previous hypothesis that slow boot is present on all computers.

<img width="2048" height="1536" alt="image" src="https://github.com/user-attachments/assets/9211c740-f715-4d52-825e-af0ce8264654" />

## Security Audit ##
The following screenshot of the security Audit shows us all the vulnerabilities that are present in the system. While some may not be active , they show that we need to improve the overall of security of the system of the PC. It lacks ways to scan for malware ,with the addition of the lack of other features that could enrich our systems overall reliability and consistency. 

<img width="1280" height="575" alt="image" src="https://github.com/user-attachments/assets/85c671e3-25da-49a3-b777-b08a6219832a" />

<img width="1280" height="575" alt="image" src="https://github.com/user-attachments/assets/8b661168-da18-4aa2-9218-4ee09185e94e" />

<img width="1280" height="575" alt="image" src="https://github.com/user-attachments/assets/473f9b00-732b-471c-ae6d-d3253424179e" />

<img width="1280" height="575" alt="image" src="https://github.com/user-attachments/assets/0087bd70-1995-410a-9b86-4e77b6495a3f" />

## Root Cause ##
Slow processes are mainly caused by slow HDD and RAM as they are the most lacking in each computer system. While 1 monitor had an issue with cabling that caused wrong colours. Lastly is slow network which caused installing tools to shorten our investigation time by waiting for network to operate again

## Recommendations ##
The next investigation stage should focus on the areas that are not yet evidenced. Storage should be changed to SSD for faster times and startup times. The next would be adding more RAM for more multitasking and processing. Next is getting better internet for faster research and reliable connections. Lastly, monitor changes and move away from
VGA cables as they are not good enough as a cabling anymore and hard for others to find root causes.

## Overall Findings ##
The investigation establishes a clear baseline for the Dell Vostro 260 and adds useful dynamic evidence from Linux monitoring and stress tests. The BIOS confirms the platform, processor, memory and storage configuration. lscpu confirms four CPU cores, a 1.6–3.4 GHz frequency range, VT-x and the displayed cache structure. htop shows live CPU and memory behavior, while the stress tests completed successfully. The observed CPU temperatures remained around 51–58°C during the photographed load periods. No failure was reproduced in these short tests, so further investigation should concentrate on storage health, system logs, application behavior and power-related evidence.

## Commands used ##
•lscpu

•htop

•vtop

•stress --cpu 4 --timeout 60

•stress --vm 2 --vm-bytes 256M --timeout 30

•stress --cpu 2 --io 2 --timeout 45

•sudo smartctl -H /dev/sda

•sudo smartctl -a /dev/sda

•systemd-analyze

•speedtest

•ip link show

•ip route show

•sudo apt install lynis

•sudo lynis audit system

## Tags and Codes ##
Only User05 had these shown :

Service Tag:C4L095J

Express Service Code: 2639536535
