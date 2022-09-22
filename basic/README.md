# Building an Execution Environment

This example demonstrates how to build a basic execution environment. During the 
build system packages will be installed which are defined in the _bindep.txt_ file. 
Python modules will be included from the _requirements.txt_ file. Finally any 
Ansible collections will be added from the _requirements.yml_ file.

You can build the execution environment with the following command.

```console
ansible-builder build -t basic-ee
```
