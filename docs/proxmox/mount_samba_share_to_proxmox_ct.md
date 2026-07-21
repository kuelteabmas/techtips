# Mount Samba Share to Proxmox Container

*Monday, July 20th, 2026* by **devP**

### Main Goal: Mount on the Proxmox host, then bind-mount into the CT

1. On the Proxmox host (not inside the CT), create a mount point and credentials file:

```
mkdir -p /mnt/smbShareDir
mkdir -p /root/.smbcreds

cat > /root/.smbcreds/smbShareDir <<EOF
username=youruser
password=yourpassword
domain=WORKGROUP
EOF
chmod 600 /root/.smbcreds/smbShareDir
```

2. Add to the host's /etc/fstab:

```
//<server-ip>/smbShareDir  /mnt/smbShareDir  cifs  credentials=/root/.smbcreds/smbShareDir,iocharset=utf8,vers=3.0,uid=100000,gid=100000,file_mode=0770,dir_mode=0770  0  0
```

Note the uid=100000,gid=100000 — for an unprivileged CT, root inside the container (uid 0) maps to uid 100000 on the host. Setting the mount's ownership to 100000 means the CT's root user will actually be able to read/write it. Adjust if your CT uses a different ID mapping (check /etc/subuid on the host).
3. Mount it on the host:
bashmount -a
`df -h | grep smbShareDir`

4. Add a bind-mount into the CT config. On the Proxmox host, edit `/etc/pve/lxc/<CTID>.conf` (find your CTID with pct list):
```
nano /etc/pve/lxc/<CTID>.conf
```
Add a line:

`mp0: /mnt/smbShareDir,mp=/mnt/smbShareDir` 

5. Restart the container:
```
pct stop <CTID>
pct start <CTID>
```
Now `/mnt/smbShareDir` should just appear inside the CT already mounted, no CIFS mount attempt needed from inside it at all — and it'll be visible to Docker containers running inside the CT too, since it's a normal filesystem path from their perspective.