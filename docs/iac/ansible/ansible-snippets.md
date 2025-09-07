# Ansible Snippets

```

- name: Create smbcredentials file with rw permission for username
  ansible.builtin.file:
    path: "/home/{{ username }}/smbcredentials"
    state: touch
    mode: "666"
  when: "'mediaserver' in inventory_hostname"

- name: Add smbcredentials file contents
  become_user: "{{ username }}"
  ansible.builtin.shell:    
    cmd: echo "username={{ smb_username }} \npassword={{ smb_password }}" > ~/smbcredentials
  when: "'mediaserver' in inventory_hostname"

```