# Separate production and staging inventory

You can keep your production environment separate from all your other environments by using parted inventory files or even directories for each environment.

This makes the inventory files clearer and they don't get too cluttered over time. You can also combine multiple inventory source types in an inventory directory. This can be useful for combining static and dynamic hosts and managing them as one inventory.

## Bad

Folder structure:

```bash
/path/to/your/ansible
├── ansible.cfg
├── group_vars
├── host_vars
├── inventory_file
├── playbooks
├── roles
```

File structure:

```yaml
[example_test_web]
example_test_web01

[example_live_web]
example_live_web01

[example_live:children]
example_live_web

[example_test:children]
example_test_web

```

## Good

Folder structure

```bash
/path/to/your/ansible
├── ansible.cfg
├── inventory
└── live
│   ├── group_vars
│   └── host_vars
└── test
    ├── group_vars
    └── host_vars
├── playbooks
├── roles
```

File structure:

inventory/live:

```yaml
[example_live_web]
example_live_web01

[example_live:children]
example_live_web
```

inventory/test:

```yaml
[example_test_web]
example_test_web01

[example_test:children]
example_test_web
```
