# Building an execution environment

This example demonstrates how to build a basic execution environment. During the
build packages in _bindep.txt_, Python modules in _requirements.txt_, and Ansible
collections in _requirements.yml_ will install into the execution environment.

You can build the execution environment with the following command.

```console
ansible-builder build --prune-images -t basic-ee
```
