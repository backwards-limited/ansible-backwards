# Ansible Introduction

We'll be using the Ubuntu VM previously setup.

First, the Ansible configuration file - where to find it, in the following order:

- Ansible_Config - environment variable
- sensible.cfg - current directory
- .ansible.cfg - in user's home
- /etc/ansible/ansible.cfg - default settings, plus docs

Choose some directory to work in e.g.:

```bash
$ pwd
/home/davidainslie/code/ansible-course
```

Let's begin with a simple configuration:

```bash
$ vim ansible.cfg
```

```properties
[defaults]
host_key_checking = False
```

To see all possible configuration:

```bash
$ less /etc/ansible/ansible.cfg

# config file for ansible -- https:/ansible.com/
...
```

Next configuration is the **hosts** file or **inventory** file i.e. which hosts ansible will manage e.g.

```properties
[allservers]
10.0.3.107
10.0.3.35

[web]
10.0.3.107
```

Create an inventory file with the IPs of our running containers:

```bash
$ lxc-ls -f
NAME   STATE     AUTOSTART   GROUPS   IPV4         IPV6   UNPRIVILIGED
db1    RUNNING   0           -        10.0.3.167   -      false
web1   RUNNING   0           -        10.0.3.86    -      false
web2   RUNNING   0           -        10.0.3.229   -      false
```

```bash
$ vim inventory
```

```properties
[allservers]
10.0.3.167
10.0.3.86
10.0.3.229

[database]
10.0.3.167

[web]
10.0.3.86
10.0.3.229
```

Again, we can look at the default file for examples:

```bash
$ less /etc/ansible/host

# This is the default ansible 'hosts'file.
...
```

