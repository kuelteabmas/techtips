# Linux Troubleshooting

### Scenario
> Received disconnect from 192.168.1.87 port 22:2: Too many authentication failures
> Disconnected from 192.168.1.87 port 22

Temporary resolve this by running in order log in via SSH:
`ssh -o IdentitiesOnly=yes 192.168.1.87 ` 


##### To permanently fix this 

If you SSH into your host with verbose enabled, you'll find that multiple keys are being used to log into your host.
`ssh -vvv hostname`

In order to resolve this error, you need to explicitly specify to use the SSH key and enable `IdentitiesOnly` within the `~/.ssh/config`

``` 
Host 10.85.194.165
  IdentityFile ~/.ssh/id_edcsa
  IdentitiesOnly yes
  Port 22
```

SSH'ing again should work.
___

### Scenario

>Remove SSH key from know_hosts

`ssh-keygen -R hostname`

___

### Scenario

>W: Target Packages (pve-no-subscription/binary-amd64/Packages) is configured multiple times in /etc/apt/sources.list.d/pve-community.list:1 and /etc/apt/sources.list.d/pve-no-subscription.list:1

***Source**: https://askubuntu.com/questions/760896/how-can-i-fix-apt-error-w-target-packages-is-configured-multiple-times#762815* 


There's is a Python script to automate this task. You can find the most recent version here.
Installation:

1. Install the prerequisites:
`sudo apt install python3-apt`

1. Download the PYZ bundle (aptsources-cleanup.pyz) from the latest release.
`wget https://github.com/davidfoerster/aptsources-cleanup/releases/download/<version>/aptsources-cleanup.pyz`

1. Mark the PYZ bundle as executable:
`chmod a+x aptsources-cleanup.pyz`

**Usage:**

From the download location of the PYZ bundle (see step 2 above) run:

`sudo ./aptsources-cleanup.pyz`

Follow the instructions appearing on the screen.
