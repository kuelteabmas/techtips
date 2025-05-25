# Adding and Extending 2nd Drive to Existing Volume Group 
Satuday, May 24th, 2025* by **devP**


> This can help extend local-lvm and allow more VM disk space

New Drive: `/dev/nvme1n1`

Create partition with fdisk or via GUI
Should have new partition as: `/dev/nvme1n1p1`

Run `vgs` to view all Volume Groups if needed to check corrent VG

Run following commands to extend current VG (default VG name: `pve`)

Create Physical Volume for new disk
`pvcreate <mount point>`
* ie: `pvcreate /dev/sda1`

Extend VG 
`vgextend <VG> <mount point>`
* ie: `vgextend pve /dev/sda1`

Extend Logical Volume to size of new drive
`lvextend /dev/pve/data -L <size of Physical Volume>`
* ie: `lvextend /dev/pve/data -L +930g`

Display all Volume Groups
`lvdisplay`
