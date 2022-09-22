# Accessing Collections from Red Hat Automation Hub

While building this execution environment you will include Ansible collections
that are hosted on [Red Hat Automation Hub](https://console.redhat.com/ansible/automation-hub).

In order to access Red Hat Automation Hub you must create a token to include in
the _ansible.cfg_ configuration file.

Log into [https://console.redhat.com](https://console.redhat.com) with your Red Hat
portal credentials. Then visit the [Connect to Hub](https://console.redhat.com/ansible/automation-hub/token)
page. Click the button 'Load token', this will generate a token for you. Copy it
and edit the _ansible.cfg_ file in the _ee_ directory. Uncomment the `token` line
and paste your token. Save the file and exit.

You can build the execution environment with the following command.

```console
ansible-builder build -t automationhub-ee
```
