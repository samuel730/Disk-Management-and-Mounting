# Linux Disk Management & Mounting 

## Project Overview

This project demonstrates essential Linux system administration and DevOps skills, focusing on disk management, partitioning, filesystem creation, and mounting using a loop-based virtual disk in a WSL (Windows Subsystem for Linux) environment.

It simulates real-world storage management tasks performed by DevOps and system engineers on Linux servers.

---

## Objectives

- Create and manage virtual disks using loop devices
- Perform disk partitioning using `fdisk`
- Format partitions with the ext4 filesystem
- Mount and verify filesystems
- Retrieve UUIDs for persistent storage configuration
- Simulate real Linux server storage operations in WSL

---

## Tools & Technologies

- Linux (WSL Ubuntu)
- Bash Shell
- fdisk
- mkfs.ext4
- losetup
- lsblk
- mount / umount
- blkid
- df

---

## Project Steps

### 1. Create Virtual Disk Image
A 500MB disk image was created to simulate a physical disk.

```bash
sudo fallocate -l 500M /mnt/disk.img
```

<img width="1232" height="194" alt="image" src="https://github.com/user-attachments/assets/c0d5fcbe-e6c5-4ed7-8193-6e74b015201f" />

### 2. Attach Disk as Loop Device
```
sudo losetup -fP /mnt/disk.img
losetup -a
````

<img width="1274" height="154" alt="image" src="https://github.com/user-attachments/assets/a8f87b36-ba27-4a7b-9296-938a512d86fd" />

### 3. Identify Disk
```
lsblk
```
Example:
```
loop0  500M disk
└─loop0p1  499M part
```

<img width="1200" height="332" alt="image" src="https://github.com/user-attachments/assets/0f8c1893-69b2-4489-85ac-40be67dbedf4" />

### 4. Create Partition
```
sudo fdisk /dev/loop0
```
Steps inside fdisk:

- n → new partition
- p → primary
- default values
- w → write changes

<img width="1216" height="1126" alt="image" src="https://github.com/user-attachments/assets/aef0ba3d-e46a-4c68-b2bf-5fee3cff9108" />

### 5. Format Partition (ext4)
```
sudo mkfs.ext4 /dev/loop0p1
```

<img width="1250" height="524" alt="image" src="https://github.com/user-attachments/assets/af0e16dc-2d41-45b4-be99-d5609b9656fc" />

### 6. Create Mount Point
```
sudo mkdir -p /mnt/mydisk
```

<img width="1220" height="92" alt="image" src="https://github.com/user-attachments/assets/2558c794-e390-444f-83e0-01f05ed2eb3f" />

### 7. Mount Partition
```
sudo mount /dev/loop0p1 /mnt/mydisk
```

<img width="1244" height="72" alt="image" src="https://github.com/user-attachments/assets/d3f22aa0-b871-42c2-9421-8658a99cdffe" />

### 8. Verify Mount
```
df -h
lsblk
```

<img width="1226" height="920" alt="image" src="https://github.com/user-attachments/assets/9e08e01a-e629-4ecd-a505-3260365bc331" />

<img width="1218" height="348" alt="image" src="https://github.com/user-attachments/assets/347cf9ea-bafa-4079-a415-67f05c75ae4c" />

### 9. Test File Creation
```
echo "Disk Management Lab Completed" | sudo tee /mnt/mydisk/test.txt
```

<img width="1228" height="116" alt="image" src="https://github.com/user-attachments/assets/a3eba215-a204-4c8c-9626-6092c4b50a11" />

### 10. Retrieve UUID
```
sudo blkid /dev/loop0p1
```
Example:
```
UUID=a86cdaab-e960-4500-9c50-7e793264c8bd
```

<img width="1242" height="152" alt="image" src="https://github.com/user-attachments/assets/7a598f08-184a-4c77-96e6-9cb9a4ad054d" />

### 11. Configure Persistent Mount (fstab)
```
sudo nano /etc/fstab
````
Add:
```
UUID=a86cdaab-e960-4500-9c50-7e793264c8bd  /mnt/mydisk  ext4  defaults  0  0
```

<img width="1208" height="76" alt="image" src="https://github.com/user-attachments/assets/06d212f9-4f5d-4eaa-9e0f-6197fdd70c85" />

### Verification Output
- Disk successfully created and partitioned
- Filesystem formatted as ext4
- Mounted at /mnt/mydisk
- File write test successful
- UUID retrieved for persistence
### Key Learnings
- Linux disk structure and partitioning
- Loop device simulation for storage testing
- Filesystem formatting and mounting process
- Persistent storage configuration using /etc/fstab
- Real-world DevOps storage management workflow

## 📌 Conclusion

This project successfully demonstrated the complete lifecycle of disk management in Linux, including disk creation, partitioning, filesystem formatting, mounting, and verification. Using a loop-based virtual disk in a WSL environment, we were able to safely simulate real-world storage operations without requiring physical hardware.

The exercise reinforced key DevOps and system administration concepts such as working with `fdisk`, `mkfs.ext4`, `mount`, and `lsblk`, as well as understanding how to retrieve UUIDs for persistent configuration using `/etc/fstab`. These skills are essential for managing storage systems in Linux servers, cloud environments, and production infrastructure.

Overall, this lab provides a strong foundation for real-world DevOps tasks involving storage management, system setup automation, and Linux administration.




























