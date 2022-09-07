# Use native YAML syntax for your Ansible code

There are several ways you can write your code in Ansible. At its core, the Ansible playbook runner is a YAML parser with added logic such as:

```
commandline key=value
```

## Bad

Using the key=value shorthand format will limit the readability of your code:

```yaml
- name: install telegraf
  ansible.builtin.yum:
    name: telegraf-{{ telegraf_version }} state=present update_cache=yes disable_gpg_check=yes enablerepo=telegraf
  notify: restart telegraf

- name: configure telegraf
  ansible.builtin.template: src=telegraf.conf.j2 dest=/etc/telegraf/telegraf.conf
  notify: restart telegraf
```

## Good

Using native YAML has a few more lines but it reduces horizontal scrolling and line wrapping. Another benefit is the improved syntax highlighting in modern text editor software.

```yaml
- name: install telegraf
  ansible.builtin.yum:
    name: telegraf-{{ telegraf_version }}
    state: present
    update_cache: yes
    disable_gpg_check: yes
    enablerepo: telegraf
  notify: restart telegraf

- name: configure telegraf
  ansible.builtin.template:
    src: telegraf.conf.j2
    dest: /etc/telegraf/telegraf
```
