# Using Ansible development tools

Workshop demonstrating the use of Ansible development tools such as `ansible-navigator`
and `ansible-builder`.

>**NOTE**: These examples were tested on a RHEL 8 and 9 systems with `podman`.

## Using ansible-builder

Install the `ansible-builder` package with the `pip` command.

```shell
pip install --user ansible-builder
```

Then create a working directory, which has the file _execution-environment.yml_.
This is the configuration file that `ansible-builder` will use to build the container
image.

The following is an example of an _execution-environment.yml_ file.

```yml
---
version: 3

ansible_config: ansible.cfg

dependencies:
  galaxy: requirements.yml
  python: requirements.txt
  system: bindep.txt

images:
  base_image:
    name: registry.redhat.io/ansible-automation-platform-24/ee-minimal-rhel9:latest

options:
  package_manager_path: /usr/bin/microdnf
```

- The _base_image_ parameter specifies the execution environment container image
   to use as the starting point.
- The optional _ansible.cfg_ parameter specifies the Ansible configuration file.
- The _galaxy_ parameter specifies the file that lists the collections to install.
- The _python_ parameter specifies the file that lists the Python packages to install.
- The _system_ parameter specifies the file that lists the packages to install.
- The _package_manager_path_ parameter specifies the package manager to use.

Example of the _requirements.yml_ file:

```yml
---
collections:
  - community.general
  - community.aws
```

Example of the _requirements.txt_ file:

```txt
awxkit
cryptography>=35.0.0
```

Example of the _bindep.txt_ file:

```txt
gcc [platform:rpm]
```

## Building an execution environment

Using your Red Hat Portal credentials login into the Red Hat Container Registry.

```shell
podman login registry.redhat.io
```

This will allow for the container images defined in _execution_environment.yml_ to
pull from the registry during the build.

Once you have your files in your working directory you can use the  `ansible-builder`
command, use the _--tag_ or _-t_ option to create your container a name.

```shell
ansible-builder build --tag ee-custom:v1.1
```

You can use `podman images` to display your local containers.

## Automation content navigator

To install `ansible-navigator` in your environment use the
`pip` command.

```shell
pip install --user ansible-navigator
```

Use the `ansible-navigator` command to run the automation content navigator. If you
run the command with no arguments it will start in interactive mode.

Several Ansible commands have an equal navigator subcommand.

| **Ansible Command** | **Navigator Subcommand** |
| --- | --- |
| `ansible-config` | `ansible-navigator config` |
| `ansible-doc` | `ansible-navigator doc` |
| `ansible-inventory` | `ansible-navigator inventory` |
| `ansible-playbook` | `ansible-navigator run` |

Navigator also provides additional functionality.

| **Subcommand** | **Description** |
| --- | --- |
| collections | Get information about installed collections. |
| config | Examine current Ansible configuration. |
| doc | Examine Ansible documentation for a plugin. |
| help | Detailed help for `ansible-navigator`. |
| images | Examine an execution environment. |
| inventory | Explore an inventory. |
| log | Review the current log file. |
| open | Open the current page in a text editor. |
| replay | Replay a playbook artifact. |
| run | Run a playbook.|
