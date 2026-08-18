
# Kubernetes Troubleshooting
Tuesday, August 18th, 2026* by **devP**


Run this command to help debug whether 
- a site is reachable from your LoadBalancer 
- could be to check HTTP/HTTPS
- to rule out network/VLAN routing issues
 `k run -it --rm debug --image=curlimages/curl --restart=Never -n traefik -- curl -vk https://192.168.12.177:8000`

 Once completed, this pod will autodeleted. 

 if successful, cli will return: 

 ```
 All commands and output from this session will be recorded in container logs, including credentials and sensitive information passed through the command prompt.
If you don't see a command prompt, try pressing enter.
pod "debug" deleted from traefik namespace
```

BusyBox debug pod logs will also show a 200 OK amond other TLS Handlshake related logs, headers, etc. 

If it fails:
```
Connecting to 192.168.12.177:8000 (192.168.12.177:8000)
wget: TLS error from peer (alert code 40): handshake failure
wget: error getting response: Connection reset by peer
pod "debug" deleted from traefik namespace
pod traefik/debug terminated (Error)
```