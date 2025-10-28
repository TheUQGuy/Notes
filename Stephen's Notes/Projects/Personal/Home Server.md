There are many possible server options for creating an AIO [[Homelab|home lab]]. The main things to consider are hardware, and software requirements.

The first consideration is what kind of tasks you would like to accomplish. What do you want to do? Do you want to: 
	-Run a video library
	-Access your smart-home remotely
	-Share your storage remotely across multiple devices
	-Host games
	-launch web applications
	-Manage databases
	-Have your own adblocker
	-Create your own dropbox clone
	-Create a sandbox for practicing new technologies
	
The sky is the veritable limit for what you can do on a server. That's not even mentioning the possibilities of multiple users using it at the same time.

Now where do we start?

## Hardware
Choosing hardware is easy, choose whatever is accessible. Got a raspberry pi? Perfect for basic media traffic. Got an old computer you are no longer using? Slap a new hard drive on that bad boy and you're all set to go. Got money? Wel- ... hmmmm.

Things get way harder the more money you have to spend on the problem. Even among budget solutions there are multiple ways to configure the same server. That's not even including the possibility of having multiple computers all being managed by a [[Hypervisor|hypervisor]]. 

There are a lot of ways to tinker with things and spending money on something that works well is paramount.

### What to consider (Hardware)
- SATA Ports
	It is a weird thing to consider at first but surprisingly enough, for large scale storage solutions or Network Attached Storage [[NAS|(NAS)]], storage is huge. Each SATA hard drive or SATA SSD takes up an additional slot. Whether you want [[RAID]] for data security and efficiency.
- CPU Considerations
	- Clock speed
		Many things run on single core/thread performance. For many game servers like minecraft, the clock speed is more relevant because the single threaded workload is easier. Any single task is much better with a higher clock speed.
	- Cores/Threads
		Cores/threads allow you to multitask with ease. Want to transcode media (like 4k video?) that requires more threads than just single clock speed. If you wanted to run multiple servers or instances of a database, multiple cores distribute the load semi-evenly.
- RAM
	The amount of ram and speed of ram is relative and equivalent. The more ram you need, the faster it should go typically speaking. Recommendation is minimum 16GB of 3200mhz ram of whatever type you need. The reason for this is that ram allows for quick storage for whatever process is currently running on your computer. The bigger the program(s) the more you will need. Some [[Pihole]] approaches literally only need the 4gb ram of a raspberry pi but for anything more robust, the ram requirements increase. 
## Software
There a lot of options for software. Not only are there a lot of OS systems but there are also a lot of plugins/addons for said OS that allow you to extend the feature list of your current rig.

There are a lot of things I want to do in my server so I will need a versatile and multipurpose OS and addons.

### What I want (software)
- I want [[NAS]] capabilities for all of my attached devices and programs
- I want to run a [[Kubernetes]] layout to practice system engineering
- I want to support multiple [[Docker]] containers
- I want to run a multimedia library
	- Films
	- Wirelessly accessible books
- I want to be able to run servers via docker
- I want to be able to integrate smart home-esque features
	- Raspberry Pi connections
	- 3d printer compatibility
- Pihole DNS adblocker
- Run minecraft server and various other game servers
- Share workload across multiple machines
- want to be able to sync data between multiple devices at least for notes
## End result
#### Hardware
For the main brain I am considering repurposing my own or custom building the main brain.

The general specs for main brain:
i7 12700kf
LGA 1700 Motherboard Mini ATX (NOT GIGABYTE) must have 4 SATA ports
64GB of DDR4 Ram
550w power supply
4x 10-20TB SATA HDDs
1x NvME M.2 SSD
CPU cooler 
Some fans I guess

For the cluster I am thinking of using the Lenovo ThinkCentre M900s. On amazon they run for $179.00 each so when purchasing 3 i should be good to run the server. I need to verify the integrity of the ram but the one I am currently looking at has a 480GB ssd and 16GB of ram which are both very useful [example](https://www.amazon.ca/Lenovo-ThinkCentre-Quad-Core-i5-6500T-Graphics/dp/B07ZPBDFGD?crid=2CBEF6XMHTFJW&dib=eyJ2IjoiMSJ9._aD7kvVSXtNVtTrTXD7c4b1l9YdFS_i43Hks9vEWM5xgWOqvE9ODeiGqjYowOLAhqFHaEf8o9sTPKBX3wT7nwm_4rHCsxRoyvyuAdPFe4gUB2ritInLgDV8buwG6pLHvlWdWTfItB6_VW6S5O6ReeeNksvI_MQmCCRYVyPsFqBFdF8ge7apNLWOR4AUEanw32lykEhDy87kE4zw_f86SM0pQtoftYTnzmGfF3heiS9wEfdNLmMh1W8_1f_hnQtG558r8wCck_CBB2hDCxdhIkAiKSAzmMdOVEqiyAAUCVQg.5VFgUOhcPs4krwQ2sajRQvrENSpYwLapgbXTdiVhLFo&dib_tag=se&keywords=lenovo%2Bmini%2Bpc&qid=1757131863&sprefix=lenovo%2Bmini%2Caps%2C148&sr=8-7&th=1) 

#### Software
The [[Kubernetes]] cluster is the most difficult part
for each Node I will try out Talos Linux

[[Proxmox]] will be my hypervisor and main OS of the motherbrain
for VMs 

[[Pihole]] will run my DNS adblocker

[[TrueNAS Scale]] to run my NAS software

[[NextCloud]] for syncing data even while not present

[[Octoprint]] for 3d printing

[[Docker]] for MC container

## TODO/Wishlist
- Dashboard: Homepage
- Ngunx Proxy manager (for remotely managing all of the ports i need)
- twingate for remote logins
- Vaultwareden for password manager
- portainer potentially can help w/ docker containers
- Octoprint helps with 3d printing
- jellyfin for media setup
- servARR is for torrenting things. IE Radarr for movies, sonarr for tv, readarr for books, bazarr for subtitles, prowlarr searches the web for content, lidarr for music, then bittorrent the rest
- NextCloud for home cloud