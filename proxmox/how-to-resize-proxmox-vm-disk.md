# Secure SSH Keygen

*Tuesday, January 2nd, 2024* by **devP**

# How to resize Proxmox VM disk and LVM partitions

1. Install parted 
`apt install parted`

2. Check disk
`fdisk -l`
`fdisk -l /dev/vda | grep ^/dev`

>
    GPT PMBR size mismatch (67108863 != 335544319) will be corrected by w(rite).
    /dev/vda1      34     2047     2014 1007K BIOS boot
    /dev/vda2    2048   262143   260096  127M EFI System
    /dev/vda3  262144 67108830 66846687 31.9G Linux LVM


3. Resize the partition 3 (LVM PV) to occupy the whole remaining space of the hard drive)
>
    parted /dev/vda
    (parted) print
    Warning: Not all of the space available to /dev/vda appears to be used, you can
    fix the GPT to use all of the space (an extra 268435456 blocks) or continue
    with the current setting? 
    Fix/Ignore? F 

    (parted) resizepart 3 100%
    (parted) quit

4. Reboot proxmox host
`reboot`
