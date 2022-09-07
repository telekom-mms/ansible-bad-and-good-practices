# Prefix your variables

You should prefix your with the name of the role (or playbook). This makes it easier to know where the variable is used.

Here’s an example. Imagine you’re writing a role to install and configure the Apache web-server (you probably don’t have to). The role is named `apache`.
Now you want to create a variable that configures the default Listen-port.

## Bad

```yaml
- hosts: localhost
  vars:
    listen_port: 443
  tasks:
    - name: configure apache
      ansible.builtin.template:
        src: httpd.conf.j2
        dest: /etc/httpd/conf/httpd.conf
```

## Good

```yaml
- hosts: localhost
  vars:
    apache_listen_port: 443
  tasks:
    - name: configure apache
      ansible.builtin.template:
        src: httpd.conf.j2
        dest: /etc/httpd/conf/httpd.conf
```

Other than the reason mentioned earlier, there’s no ambiguity here. You definitely know that this variable belongs to the apache-role. There could be another role for some other kind of software that also defines a listen-port. With prefixed variables this is not a problem since variables have their own namespace now.

By the way, Puppet and Chef are on the advantage here, having namespaces for their roles. Ansible is not designed this way.
