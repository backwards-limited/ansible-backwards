# Ansible Introduction

We'll be using the Ubuntu VM previously setup.

First, the Ansible configuration file - where to find it, in the following order:

- Ansible_Config - environment variable
- sensible.cfg - current directory
- .ansible.cfg - in user's home
- /etc/ansible/ansible.cfg - default settings, plus docs

Let's begin with a simple configuration:

We'll create a directory to hold our ansible files and use it as a "working directory".

```bash
$ mkdir ansible
```

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
$ sudo lxc-ls -f
NAME   STATE     AUTOSTART   GROUPS   IPV4         IPV6   UNPRIVILIGED
db1    RUNNING   0           -        10.0.3.167   -      false
web1   RUNNING   0           -        10.0.3.86    -      false
web2   RUNNING   0           -        10.0.3.229   -      false
```

```bash
$ vim hosts.ini
```

```properties
[allservers]
10.0.3.167 ansible_connection=local
10.0.3.86 ansible_connection=local
10.0.3.229 ansible_connection=local

[database]
10.0.3.167 ansible_connection=local

[web]
10.0.3.86 ansible_connection=local
10.0.3.229 ansible_connection=local
```

Again, we can look at the default file for examples:

```bash
$ less /etc/ansible/host

# This is the default ansible 'hosts'file.
...
```

## Ad-Hoc Commands

```bash
$ ansible <group/machine> -m module -a <args> (-k for ask-pass)
```

```bash
$ sudo lxc-ls -f
NAME   STATE     AUTOSTART   GROUPS   IPV4         IPV6   UNPRIVILIGED
db1    RUNNING   0           -        10.0.3.167   -      false
web1   RUNNING   0           -        10.0.3.86    -      false
web2   RUNNING   0           -        10.0.3.229   -      false
```

#### Ping

```bash
$ ansible 10.0.3.229 -m ping -i hosts.ini
```

where **-i** is for **inventory**. But the result might be:

```bash
10.0.3.229 | UNREACHABLE
...
```

Create an ssh key and add:

```bash
$ ssh-agent bash

$ ssh-keygen -t rsa

$ ssh-add ~/.ssh/id_rsa

$ ssh-copy-id -i ~/.ssh/id_rsa ubuntu@10.0.3.229
```

```bash
$ ansible 10.0.3.229 -m ping -i hosts.ini
10.0.3.229 | SUCCESS
...
```

P.S. We can add a user to the remote users via the default installed **ubuntu** user e.g.

```bash
$ ssh ubuntu@10.0.3.229

$ sudo adduser davidainslie
```

```bash
$ ssh davidainslie@10.0.3.229
```

We can ping a **group**:

```bash
$ ansible web -m ping -i hosts.ini
10.0.3.229 | SUCCESS
...
10.0.3.86 | SUCCESS
...
```

```bash
$ ansible allservers -m ping -i hosts.ini
```

Ping as some **user**:

```bash
$ ansible allservers -m ping -i hosts.ini -u root
```

#### APT-GET

Let's install **nginx** on our web servers:

```bash
$ sudo ansible web -a "apt-get update" -i hosts.ini
```

```bash
$ sudo ansible web -a "apt-get -y install nginx" -i hosts.ini
```

and check:

```bash
$ sudo ansible web -m service -a "name=nginx state=restarted" -i hosts.ini
```



