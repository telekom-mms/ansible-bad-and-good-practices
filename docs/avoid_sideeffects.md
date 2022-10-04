# Avoid unintended side effects when running playbooks

When writing tasks that can target different environments, make sure that the playbook-run only targets the environments that you really want to change.


## Bad

Suppose you have a list of environments defined in the `group_vars`:

```yaml
environments:
  - dev
  - qa
  - prod
```

In the playbook you can delete databases based on the environment:

```yaml
---
- hosts:
    - localhost
  vars:
    db_list_backend:
      - cms
      - fms
  tasks:
    - name: Drop all backend databases
      community.mysql.mysql_db:
        login_user: mysqlroot
        login_password: "password"
        login_host: "mysqlserver"
        name: "{{ item.0 }}"
        state: absent
      loop: "{{ db_list_backend | product(environments) }}"
```

Then you would need to call the playbook like this to only delete databases on the dev-environment:

```yaml
ansible-playbook playbook.yaml --extra-vars='{environments: [dev]}'
```

But what would happen if you ran the playbook without the `extra-vars`? All environments would be deleted - probably not what you'd expect.

## Good

Instead of relying on the `environments` variable being correctly set, you can do two things:

* Use a `vars_prompt` to ask for the environment to be deleted.
* Since you cannot define allowed variables in a `vars-prompt`, you can use an `assert`-task to check for allowed values. This way, you cannot accidentally delete the production databases.

```yaml
---
- hosts:
    - localhost
  vars:
    db_list_backend:
      - cms
      - fms
    allowed_environments:
      - dev
      - qa
  vars_prompt:
    - name: db_environment
      prompt: "Attention: This will delete all databases in the desired environment! Please enter the environment (dev, qa):"
  tasks:
    - name: Assert that db_environment is allowed environment
      ansible.builtin.assert:
        that: db_environment in allowed_environments
        fail_msg: "{{ db_environment }} is not a valid environment"
      tags:
        - always

    - name: Drop all backend databases
      community.mysql.mysql_db:
        login_user: mysqlroot
        login_password: "password"
        login_host: "mysqlserver"
        name: "{{ item }}"
        state: absent
      loop: "{{ db_list_backend }}"

```

The final `ansible-playbook` call would look like this:

```bash
ansible-playbook playbook.yaml --extra-vars="db_environment=dev"
```
