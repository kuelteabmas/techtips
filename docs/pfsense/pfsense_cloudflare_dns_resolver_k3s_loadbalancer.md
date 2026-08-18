# Adding LAN and outside LAN Access DNS Resolver for Cluster wide hosted services via a Load Balancer
Monday, August 17th, 2026* by **devP**

### Inside LAN Access

For inside LAN access, add a wildcard record for your DNS resolver in order to have to access any hosted services on your cluster locally that is reachable at `<service_name>.local.YOUR_DOMAIN.com` without the need to make a call to Cloudflare for DNS. 

1. Navigate to **Services > DNS Resolver >

2. Add Custom Options (Click Show Custom Options) 
```
server:
local-zone: "local.YOUR_DOMAIN.com" redirect
local-data: "local.YOUR_DOMAIN.com A Load_Balancer_IP"
```

1. Remove any explicit Host Overrides

### Outside LAN Access
For access outside of LAN where cluster is connected to, add a `A` Record to your domain provider (ie: CloudFlare)

ie:

Type: `A`
Host: `*.local`
Content: `Load_Balancer_IP`
