# Ansible Module: diff

Some custom ansible modules not yet submitted or accepted by [Ansible](https://github.com/ansible/ansible).

## Usage

An Ansible module to do generic diffs against strings, files and command outputs.

#### Arguments

| Name             | Required | Default | Description |
|------------------|----------|---------|-------------|
| source           | Yes      |         | The source input to diff. Can be a string, contents of a file or output from a command, depending on `source_type` |
| target           | Yes      |         | The target input to diff. Can be a string, contents of a file or output from a command, depending on `target_type` |
| source_type      | No       | string  | Specify the input type of `source`: `string`, `file` or `command` |
| target_type      | No       | string  | Specify the input type of `target`: `string`, `file` or `command` |
| diff             | No       | raw     | Specify the diff type: `raw` or `yaml`. |
| diff_yaml_ignore | No       | `[]`    | List of keys to ignore for yaml diff |


#### Examples

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

# Diff compare two normalized yaml files (sorted keys and comments stripped),
# but additionally ignore the yaml keys: 'creationTimestamp' and 'metadata'
- diff:
    source: /tmp/file-1.yml
    target: /tmp/file-2.yml
    source_type: file
    target_type: file
    diff: yaml
    diff_yaml_ignore:
      - creationTimestamp
      - metadata
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
