# Name your tasks and plays

When writing tasks and plays in Ansible naming them is optional. However you should always give useful names to your tasks ands plays.

## Bad

When you run a playbook without named tasks, you’ll see the following output.

```
- hosts: all
  tasks:
    - ansible.builtin.include_vars: foo.yml
    - ansible.builtin.yum:
        name: httpd
```

```bash
PLAY [localhost]
********************************

TASK [include_vars]
********************************
ok: [localhost]

TASK [yum]
********************************
ok: [localhost]
```

## Good

When trying to debug failed tasks it’s really helpful to actually know what task failed and what the task should have been doing. Assigning names to your taks will give the following output.


```bash
- name: install apache
  hosts: all
  tasks:
    - name: include the config vars for the apache
      ansible.builtin.include_vars: foo.yml
    - name: install apache with yum
      ansible.builtin.yum:
        name: httpd
```

```bash
PLAY [install apache]
********************************

TASK [include the config vars for the apache]
********************************
ok: [localhost]

TASK [install apache with yum]
********************************
ok: [localhost]
```
