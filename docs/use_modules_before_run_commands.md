# Use Modules Before Run Commands

Ansible is batteries-included and comes with more than **6000** modules to help manage systems. Most times it’s not needed (nor useful!) to fall back to shell commands instead of using modules.

## Bad

```
- name: install htop
  hosts: all
  tasks:
    - name: install htop
      ansible.builtin.command: "yum install htop -y"
```

## Good

```
- name: install htp
  hosts: all
  tasks:
    - name: install htop
      ansible.builtin.yum:
        name: "htop"
        state: present
```


Ansible is helpful in detecting when you should use modules instead of commands. It detects these uses and prints a warning. When running the above task with command Ansible prints:

```
TASK [command] ***********************
 [WARNING]: Consider using yum module rather than running yum
```
