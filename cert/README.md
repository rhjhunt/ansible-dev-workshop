# Adding content to an execution environment

In this example we will be adding a custom CA certificate to the execution environment.

You can add your own CA if you have one or you can use the provided __create_ca_cert.yml__
playbook.

Due to the requirements from the playbook for the _community.crypto_ collection and
the `cryptography` python module use the execution environment from the basic build
to run this playbook.

```console
 ansible-playbook create_ca_cert.yml
 WARNING]: provided hosts list is empty, only localhost is available. Note that
the implicit localhost does not match 'all'

PLAY [Generate a self-signed CA] ***********************************************

TASK [Gathering Facts] *********************************************************
ok: [localhost]

TASK [Create CA root key] ******************************************************
changed: [localhost]

TASK [Create CA CSR for self-signed certificate] *******************************
changed: [localhost]

TASK [Create CA self-signed certifice from CSR] ********************************
changed: [localhost]

PLAY RECAP *********************************************************************
localhost: ok=4    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

This will generate 3 files in your current working directory.

```console
ca.cert.csr  ca.cert.pem  ca.key.pem
```

```console
cd ee/
ansible-builder create
cp ../ca.cert.pem context/
```

You can now build the execution environment and include the CA certificate.

```console
ansible-builder build -t cert-ee
```
