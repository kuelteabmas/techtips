# Jenkins Notes

*Monday, March 3rd, 2025* by **devP**

### Permissions
Add `jenkins` user to `docker` group if `docker` commands will be performed during Jenkins build

1. Log into VM or LXC hosting Jenkins instance
2. Run: `usermod -aG docker jenkins`