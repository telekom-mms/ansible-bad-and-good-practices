# Ansible - Good and Bad Practices

A collection of good and bad Ansible code examples.

* [Name your tasks](docs/name_your_tasks.md)
* [Use Modules before run-commands](docs/use_modules_before_run_commands.md)
* [Use native yaml syntax](docs/use_native_yaml_syntax.md)
* [Use the copy-module or template-module instead of lineinfile-module](docs/use_copy_template_instead_of_lineinfile.md)
* [Avoid unintended side effects when running playbooks](docs/avoid_sideeffects.md)
* [Turn off gather_facts if not needed](docs/turn_off_gather_facts.md)
* [Prefix your variables](docs/prefix_your_variables.md)

## Contributing

If you want to contribute you can create a merge request so other colleagues will discuss the code with you. Make sure to add both a good and a bad practice to your code example.

Make sure that:
- your code won't contain credentials
- you've commented the code why it is a good or bad practice
- your code can be easily run, so please add a full playbook if possible
- be open to discuss with your colleagues

If you want to change, discuss or view the code - feel free to visit the repository: [https://github.com/telekom-mms/ansible-bad-and-good-practices](https://github.com/telekom-mms/ansible-bad-and-good-practices)
