# Networking Tools

## telnet
> Telnet is a network protocol used to virtually access a computer and provide a two-way, collaborative and text-based communication channel between two machines.

`telnet IP_ADDRESS PORT_NUMBER` 


```
telnet 154.159.83.91 412

Trying 154.159.83.91...
Connected to 154.159.83.91.
Escape character is '^]'.

```

## ethtool
> **ethtool** is the primary means in Linux kernel-based operating systems for displaying and modifying the parameters of network interface controllers and their associated device driver software from application programs running in userspace.

##### Identify a port
`ethtool -p enps10 15`
`ethtool --idetify enps10`
