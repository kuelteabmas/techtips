# Common Linux Commands

##### Shutdown immediately
`sudo shutdown -P now` 

##### View Logs
`tail -f /var/log/kern.log`

##### Create a new user, add to `sudo` group, assign `bash` shell, and add as a system user:
*  `useradd -m -g sudo -s /usr/bin/bash -r john`
   * `g sudo`: add to `sudo` group 
   * `-s /usr/bin/bash`: assign bash shell
   * `r`: system user
