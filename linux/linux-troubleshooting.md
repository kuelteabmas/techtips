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
