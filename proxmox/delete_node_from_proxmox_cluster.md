# How to delete a Node from a Proxmox Cluster

*Monday, January 27th, 2025* by **devP**

1. ssh into root of a node that will remain in the cluster.
2. list node if necessary
`pvecm nodes`

3. delete node
`pvecm delnode node_to_delete`

4. remove node folder in `/etc/pve/nodes`
`rm -R /etc/pve/nodes/node_to_folder`

4. reboot