# Ansible Module: diff

Some custom ansible modules not yet submitted or accepted by [Ansible](https://github.com/ansible/ansible).

## Usage

An Ansible module to do generic diffs against strings, files and command outputs.

**Task Examples**

```yml
# Diff compare two strings
- diff:
    source: "foo"
    target: "bar"
    source_type: string
    target_type: string
# Diff compare variable against template file (as strings)
- diff:
    source: "{{ lookup('template', tpl.yml.j2) }}"
    target: "{{ my_var }}"
    source_type: string
    target_type: string
# Diff compare string against command output
- diff:
    source: "/bin/bash"
    target: "which bash"
    source_type: string
    target_type: command
# Diff compare file against command output
- diff:
    source: "/etc/hostname"
    target: "hostname"
    source_type: file
    target_type: command
```

## Integration

> Assuming you are in the root folder of your ansible project.

Specify a module path in your ansible configuration file.

```shell
$ vim ansible.cfg
```
```ini
[defaults]
...
library = ./library
...
```

Create the directory and copy the python module into that directory

```shell
$ mkdir library
$ cp path/to/module library
```

