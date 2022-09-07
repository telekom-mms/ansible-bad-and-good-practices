# Turn off gather_facts if you don't need it

If you execute a playbook with ```yaml
gather_facts: true ```, Ansible starts collecting facts (data from your node that is stored into variables). These details include variables from the remote host such as network configuration variables, hostnames and so on.

The collection of these facts is a time-consuming process and in order to speed up the execution of the playbook you can turn gathering facts off.

## Bad

```yaml
---
 - hosts: all
   become: true
   gather_facts: true
   tasks:
     - name: restart mysql
       ansible.builtin.service:
        name: mysql
        state: restarted
```

## Good

```yaml
---
 - hosts: all
   become: true
   gather_facts: false
   tasks:
     - name: restart mysql
       ansible.builtin.service:
        name: mysql
        state: restarted
```

Keep in mind that you need to enable gather_facts if you want to collect information about the remote host for example. A list about some of these Ansible facts can be found here: https://docs.ansible.com/ansible/latest/user_guide/playbooks_vars_facts.html#ansible-facts
