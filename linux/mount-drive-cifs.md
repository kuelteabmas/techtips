# Mount CIFS SMB Network Share

*Saturday, December 30st, 2023* by **devP**
 
Install packages
`sudo apt install cifs-utils` 

Create a dir for mount volume
`mkdir /mnt/nas_share`

Create a hidden credentials file
`touch ~/.smbcreds`

Add your credentials for share

```
username:foo
password:bar123
domain=domain
```

Give permissions and only to be read to root
`sudo chown root: ~/.smbcreds` 
`sudo chmod 600 ~/.smbcreds`

Add to `/etc/fstab` the following:
```
# <file system>             <dir>          <type> <options>                                                   <dump>  <pass>
//WIN_SHARE_IP/share_name  /mnt/win_share  cifs  credentials=~/.smbcreds,file_mode=0755,dir_mode=0755 0       0
```

Mount drives
`sudo mount -a`

Verify drives are mounted
`df -h`

```
Filesystem                     Size  Used Avail Use% Mounted on                             │
tmpfs                          794M  1.9M  792M   1% /run                                   │
/dev/sda1                       58G   11G   48G  18% /                                      │
tmpfs                          3.9G     0  3.9G   0% /dev/shm                               │
tmpfs                          5.0M     0  5.0M   0% /run/lock                              │
/dev/sda15                     105M  6.1M   99M   6% /boot/efi                              │
tmpfs                          794M  4.0K  794M   1% /run/user/1000                         │
//192.168.1.21/nas_share   47T   15T   32T  32% /mnt/nas_share 
```