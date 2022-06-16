# Using Ansible Development Tools

Workshop demonstrating the use of Ansible development tools such as `ansible-navigator`
and `ansible-builder`.

>**NOTE**: These examples were tested on a RHEL 8 system with `podman`, other versions
of RHEL/CentOS and `docker` have not been verified.

## Using ansible-builder

The `ansible-builder` packages can be installed with the `pip` command.

```shell
pip install --user ansible-builder
```

Then create a working directory, that contains the file _execution-environment.yml_.
This is the configuration file that `ansible-builder` will use to determine how
to build the container image.

The following is an example of an _execution-environment.yml_ file.

```yml
---
version: 1

build_arg_defaults:
  EE_BASE_IMAGE: registry.redhat.io/ansible-automation-platform-22/ee-minimal-rhel8:latest
  EE_BUILDER_IMAGE: registry.redhat.io/ansible-automation-platform-22/ansible-builder-rhel8:latest

ansible_config: ansible.cfg

dependencies:
  galaxy: requirements.yml
  python: requirements.txt
  system: bindep.txt
```

 - The _EE_BASE_IMAGE_ parameter declares the execution environment container image
   to use as the starting point.
 - The _EE_BUILDER_IMAGE_ parameter declares the container image that incluedes the
   tools that will be used during the build process to construct the container image.
 - The optional _ansible.cfg_ parameter specifies the Ansible configuration file.
 - The _galaxy_ parameter specifies the file that lists the collections to install.
 - The _python_ parameter specifies the file that lists the Python packages to install.
 - The _system_ parameter specifies the file that lists the RPM packeages to install.

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
cryptography==35.0.0
```

Example of the _bindep.txt_ file:

```txt
rsync [platform:rpm]
```

## Building an Automation Execution Environment

Using your Red Hat Portal credentials login into the Red Hat Container Registry.

```shell
podman login registry.redhat.io
```

This will allow for the conatiner images defined in _execution_environment.yml_ to
be pulled from the registry during the build.

Once you have your files in your working directory you can use the  `ansible-builder`
command, use the _--tag_ or _-t_ option to provide your container a name.

```shell
ansible-builder build --tag ee-custom:v1.1
```

You can use `podman images` to display your local containers.

## Automation Content Navigator

If you'd like to install `ansible-navigator` in your environment you can use the
`pip` command.

```shell
pip install --user ansible-navigator
```

Use the `ansible-navigator` command to run the automation content navigator. If you
run the command with no arguments it will start in interactive mode.

Several of the earlier Ansible commands can be replaced with the navigator subcommand.

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
| doc | Examine Ansible documentation for a plug-in. |
| help | Detailed help for `ansible-navigator`. |
| images | Examine an execution environment. |
| inventory | Explore an inventory. |
| log | Review the current log file. |
| open | Open the current page in a text editor. |
| replay | Replay a playbook artifact. |
| run | Run a playbook.|
