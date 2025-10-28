Raid is a setup that allows for extension and parity of multiple hard drives. 

RAID stands for Redundant Array of Independant Disks. It is used to create redundant data that allows for drives to continue as normal and backup if one drive fails.

#### Raid 0
All data is distributed across all of the drives at the same time. Meaning that if one drive fails, the entire stripe goes down. Very fast but almost never used because it is suboptimal.
![[Pasted image 20250901230807.png]]

#### Raid 1
Data is half of the available storage and is mirrored on the other half. When one of the drives fails, it is able to be reproduced thanks to the mirrored data on the other half of the storage. Most common raid configuration
![[Pasted image 20250901230852.png]]

#### Raid 4
One drive is used for parity which checks if data has been written over or not. It is much slower because the parity takes time to calculate and must be written over but it is functional and gives much more storage than the above methods.
  ![[Pasted image 20250901231008.png]]
#### Raid 5
It, like Raid 4, calculates and stores the parity of the drive set. The difference is that this parity is calculated and distributed across all of the drives. It is much quicker and safer than Raid 4 but only supports one hard drive failure at a given time. 
![[Pasted image 20250901231507.png]]

#### Raid 6
Same functional concept as Raid 5 but in this case there are 2 blocks of parity information spread across all of the drives. This is just in case more than 1 drive fails at the same time. It is slower than Raid 5 but it does provide that extra layer of protection in case of failure

#### Raid 10
Raid 10 is the combination of Raid 0 and Raid 1. It has stripped data which means that you get the high speeds of Raid 0 but has half of the available storage to have mirror drives that preserve the data. It gets very expensive very quickly but is the best of both worlds if money is not an issue at all.
![[Pasted image 20250901232005.png]]

## ZFS
ZFS s a way of configuring drives within a [[NAS]]. It functions basically the same as RAID in many cases

### Pools
A pool is a configuration of multiple drives together. So for example, you have 8 hard drives. You can configure them into one long ZFS Raid collection or you can split the drives into multiple smaller Pools that each contain there own Raid setups.

### Raid
#### Raidz1
Functionally the same as Raid5 where raidz1 has 1 drive with parity to repair one drive if it fails

#### Raidz2 
Raid6 equivalent with 2 drives of parity

#### 2 mirrored
Raid 10 equivalent with 2 drives mirroring 2 data drives

#### Considerations
If you lose one vdev in the pool, you lose the entire pool. Functionally this makes raidz2 the best for security and raidz1 the best cross between performance and security

### Resilvering
Resilvering is the process of mirroring the data of a failed drive to the new drive in the array. 


