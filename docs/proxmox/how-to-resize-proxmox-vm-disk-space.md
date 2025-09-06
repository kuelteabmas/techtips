# How to resize Proxmox VM partitions

*Thursday, July 4th, 2024* by **devP**

## Resize Disk by adding space to disk

First, resize your VM disk via the GUI 

> VM > Hardware > Hard Disk (scsi0) > Disk Action > Resize > Enter desired size Apply
> 
![alt text](assets/image.png)

or via commandline of your proxmox host

You can resize your disks online or offline with command line:

`qm resize <vmid> <disk> <size> `

example: to add 5G to your virtio0 disk on vmid100:

`qm resize 100 virtio0 +5G`


## Extend disk space 

- SSH into selected VM 

- Install parted if not installed
```
sudo apt install parted -y
```

- Run the following to find the drive and partitions names:
```
df -h

lsblk
```
![alt text](assets/resize-cmd-line-1.png)

- Become sudo
```
sudo su
```

Run the following:
```
parted

print
```
- If prompted, `f` for Fix (view screenshot below)


![alt text](assets/resize-cmd-line-2.png)

- Resize partition
```
resizepart 3 100%
```
![alt text](assets/resize-cmd-line-3.png)

- Exit out of parted
linux `CTRL+C` or mac `CMD+C`

- Resize physical volume
```
pvresize /dev/sda3
```
![alt text](assets/resize-cmd-line-4.png)

- Extend logical volume to 100% of free space in volume
```
lvextend -r -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
```
![alt text](assets/resize-cmd-line-5.png)

- Restart VM if changes aren't reflected