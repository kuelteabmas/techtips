# New Jenkins Instance Set Up 

*Monday, March 3rd, 2025* by **devP**

## Linux Instance Side
Add `jenkins` user to `docker` group if `docker` commands will be performed during Jenkins build

1. Log into VM or LXC hosting Jenkins instance
2. Run: `usermod -aG docker jenkins`



3. For Java build, you'll need a JDK installed

Note: Make sure that the JDK version installed corrsponds to the version required by your applications

ie: you're using Debian 12 and needs JDK 21

wget https://download.oracle.com/java/21/latest/jdk-21_linux-x64_bin.deb

sudo dpkg -i jdk-21_linux-x64_bin.deb


## Jenkins Side

Docker
github

Credentials


