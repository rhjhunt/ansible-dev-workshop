# Using Ansible Development Tools

Workshop demonstrating the use of Ansible development tools such as `ansible-navigator`
and `ansible-builder`.

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
