# Ansible Notes 
*Reference: Ansible for DevOps - Server and configuration management for humans by Jeff Geerling*

## Commands
`ansible -i hosts.ini example -m ping -u [username]`
`ansible -i hosts.ini example -a "free -h" -u [username]`

#### Verbose logs
> `-vvvv` `level 4`

`ansible-playbook run.yml -vvvv` 

#### To run a playbook
`ansible-playbook ./playbook/apt.yml -u user123 -i ./inventory/hosts`

#### To run a playbook file called run.yml
`ansible-playbook run.yml -K --ask-vault-pass`
>`-K`` will ask for the sudo password

>`--ask-vault-pass`` will ask for the vault password

*Note:* for `-K`` if enable passwordless sudo is enabled 

Don’t include the -K arg anymore only use `--ask-vault-pass` if you have an encrypted secret file for said playbook

##### Note: Or simply run to run a playbook (run.yml) with SSH key already copied to host
`ansible-playbook --ask-vault-pass run.yml`

___
#### To run a playbook (run.yml) with SSH key already copied to host and only to a specific host (server_abc) 
`ansible-playbook --ask-vault-pass run.yml -i server_abc,`
> *Note: the comma at the end of the hostname is required*

###### Given hosts file:

`[group_main]
server_abc`

___
#### Pings all hosts within current dir
`ansible all -m ping`

___

## Vagrant Commands
#### Add a Rocky Linux 8.x 64-bit ‘box’ using the vagrant box add³⁶ command:
`vagrant box add geerlingguy/rockylinux8`

#### Create a default virtual server configuration using the box you just downloaded:
`vagrant init geerlingguy/rockylinux8`

#### Boot your Rocky Linux server: 
`vagrant up`
#### Fire Up a Vagrant box
`vagrant up`

___ 

## Variables

You can put variables for each host in a folder titled `host_vars` and variables for groups in a folder named `groups_vars`
For instance, host_vars can have different SSH keys for each host

##### vars.yml:
```
username: user123
packages:
  - neofetch
  - htop
  - speedtest-cli
  - vim
  - tmux
```


For encrypted variables, you need to create a file with `ansible-vault`
Navigate to your vars folder and create it there
`cd group_vars/all`
`ansible-vault create secret.yml`

It’ll prompt for a password twice and then you can edit the file in vim and add your password
`secret-password=<password>`

You can also edit the secret file by running
`ansible-vault edit secret.yml`

To call the variable created, we use `{{ }}` within the task

From:


To:


Playbook

A Playbook is a lost of all the tasks and roles that Ansible has to execute

Running a playbook file called run.yml
ansible-playbook run.yml -K --ask-vault-pass
-K will ask for the sudo password
--ask-vault-pass will ask for the vault password

___

## Roles
Roles are basically mini playbooks
They can have their own variables, tasks, and handlers.
At the same time, they also inherit the playbook variables, so they’re
not completely isolated from the rest of the playbook.

Folder Structure for roles
[project] > Roles > System > Tasks 

___ 

## Filters
Filters in Ansible are similar to pipes in bash, and are used to
transform variables.
There are filters that can turn your variable into lowercase
or uppercase, for example
And the `password_hash` filter basically hashes our password
and ensures that the password isn't  stored in cleartext on our target machine

Ie: # hashing password with password hash filter sha512 
- name: Ensure the non-root user is created
 user:
   name: "{{ username }}"
   password: "{{ password | password_hash('sha512') }}"
___ 

## Loops

Example of a simple loop: 
- name: Ensure all necessary groups are created
 group:
   name: " {{ item }}"
 loop:
   - docker
   - samba
   - "{{ username }}"
___

## Conditionals

You can use conditionals in various places including:

#### 1. Tasks 
Add `when` within the task

example: `tasks/install.yml`
```
- name: Copy the compose file if host is server_abc
  template: 
    src: templates/compose-server_abc.yml
    dest: "{{ docker_compose_dir }}/compose.yaml"
  when: "'server_abc' in inventory_hostname"
```

When you run the command `ansible-playbook -i server_abc, run.yml`, the role will only run if the hostname `server_abc` is invoked
___

## Ansible-Galaxy

You’ll need to create a file in your main repo called `requirements.yml` and add the roles from Ansible Galaxy site in order to use them

You can add the role title in the requirements.yml as such:
---
roles:
- name: geerlingguy.docker

Then run the following command to install them:
`ansible-galaxy install -r requirements.yml`

Terminal Output
Starting galaxy role install process
- downloading role 'docker', owned by geerlingguy
- downloading role from https://github.com/geerlingguy/ansible-role-docker/archive/7.0.1.tar.gz
- extracting geerlingguy.docker to /home/user123/.ansible/roles/geerlingguy.docker
- geerlingguy.docker (7.0.1) was installed successfully

Note
You will need to add the roles to run.yml file


____

## Docker Compose files within Ansible

#### If Conditionals


**compose.yml** `roles/containers/templates/compose-mediasvr.yml`
```
services: 
# {% if "plex" in services_svr %}
  plex:
    image: lscr.io/linuxserver/plex:latest
    container_name: plex
      - /path/to/tv:/tv
    restart: unless-stopped
# {% endif %}
```

**vars.yml** 
```
services_svr:
  - plex
```

___