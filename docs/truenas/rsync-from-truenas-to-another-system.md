# Rsync from Truenas to another system

*Thursday, January 4th, 2024* by **devP**
 
`rsync -av --progress --stats truenas_IP::poolName/ /home/user/tmp/`

example: 
`rsync -av --progress --stats 192.168.1.5::photos/ /home/johnsmith/tmp/`
