# Migrating a custom Python virtual environment to a execution environment

If you are have custom Python virtual environments in Red Hat Ansible Tower you
will want to migrate those to an execution environment to use in Ansible
Automation Platform.

From your Red Hat Ansible Tower server you can list your custom virtual environments
and export the information about the Python modules installed. Which you can then use
in the _requirements.txt_ file in building the new execution environment.

```console
awx-manage list_custom_venvs
awx-manage export_custom_venv /var/lib/awx/venv/customvenv/
```

This will return output such as the following, copy this content edit the
_requirements.txt_ file to paste the information then save and exit the file.

```console
ansible==2.9.27
awxkit==21.6.0
bcrypt==4.0.0
certifi==2022.9.14
cffi==1.15.1
charset-normalizer==2.1.1
cryptography==38.0.1
idna==3.4
ipaddress==1.0.23
Jinja2==3.1.2
jmespath==1.0.1
MarkupSafe==2.1.1
psutil==5.9.2
pycparser==2.21
PyYAML==6.0
requests==2.28.1
urllib3==1.26.12
```

You are now ready to build your execution environment.

```console
ansible-builder build --prune-images -t tower-ee
```
