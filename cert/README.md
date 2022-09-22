# Adding Content to an Execution Environment

In this example we will be adding a custom CA certificate to the execution environment.

You can add your own CA if you have one or you can use the provide __create_ca_cert.yml__ 
playbook if you would like.

If you use the provide playbook you will need to install the _community.crypto_ 
collection. You can do that by running the following.

```console
ansible-galaxy collection install community.crypto
```

This collection has a requirement of the `cryptography` python module. It is available 
on Red Hat Enterprise Linux 8 as the package `python3-cryptography`. You can install
it as follows.

```console
sudo dnf -y install python3-cryptography
```

You are now prepared to run the playbook.

```console
ansible-playbook create_ca_cert.yml
```

This will generate 3 files in your current working directory.

```console
ca.cert.csr  ca.cert.pem  ca.key.pem
```

Change into the _ee_ directory and create the _context_ directory with the `ansible-builder` 
command. Then copy the _ca.cert.pem_ file into the _context_ directory. So it can
be included in the execution environment during build time.

```console
cd ee/
ansible-builder create
cp ../ca.cert.pem context/
```

You can now build the execution environment which will include the CA certificate 
that was genereated.

```console
ansible-builder build -t cert-ee
```
