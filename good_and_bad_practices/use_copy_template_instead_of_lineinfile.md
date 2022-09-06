# Use copy or template-module instead of lineinfile

It’s often necessary to change single lines in files. When having to do this, many people will use the lineinfile or blockinfile modules to change the file.

However over the years I learned that most times you should in fact not use these modules when wanting to changes files. You should rather use the template- or copy-module to manage not only single lines but the whole file itself.

The reason for that is twofold. First when using lineinfile you often have to use regex. Now you have two problems. More seriously, using regex is often okay, if the regex is simple (or you and the people using your playbooks are experienced with regex)!

The second reason is that you have to know and remember that this particular line in this config-file is managed by Ansible. If you manage the whole file with template you can use the ansible_managed-variable to show that the file is under Ansible control.

## Bad

```
- ansible.builtin.lineinfile:
    path: /etc/selinux/config
    regexp: '^SELINUX='
    line: 'SELINUX=enforcing'
```

## Good

```
- ansible.builtin.copy:
    src: "etc/selinux/config"
    dest: "/etc/selinux/config"
```

## Also Good
```
- ansible.builtin.template:
    src: "etc/selinux/config.j2"
    dest: "/etc/selinux/config"
```

with the template file looking like this:

```
# {{ansible_managed}}
SELINUX=enforcing
SELINUXTYPE=targeted
```

Bonus: you can use a variable for the selinux-state and simply change it on servers where selinux should not be in enforcing state.
