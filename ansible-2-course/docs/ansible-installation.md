# Ansible Installation

Will our VM setup and Ubuntu running, let's install Ansible. Note that on the ubuntu machine, the prompt (from our setup) will be **davidainslie@ubuntu-VirtualBox** but for brevity, we'll continue to show the ubiquitous **$** prompt:

```bash
$ sudo apt-get update
```

```bash
$ sudo apt-get install ansible
```

```bash
$ ansible --version
ansible 2.5.1
```

## Test setup - LXC

Simulate multiple servers with LXC (Linux Containers). We'll install as **root** with a **sudo -i**:

```bash
$ sudo -i
[sudo] password for davidainslie:

$ apt-get update && apt-get install lxc

$ apt-get install lxc-templates
```

Create 3 containers, 2 for web applications and another for a database. Note the use of **-t** for **template** and **-n** for **name**:

```bash
$ lxc-create -t ubuntu -n web1
##
# The default user is 'ubuntu' with password 'ubuntu'!
# Use the 'sudo' command to run tasks as root in the container.
##

$ lxc-create -t ubuntu -n web2
##
# The default user is 'ubuntu' with password 'ubuntu'!
# Use the 'sudo' command to run tasks as root in the container.
##

$ lxc-create -t ubuntu -n db1
##
# The default user is 'ubuntu' with password 'ubuntu'!
# Use the 'sudo' command to run tasks as root in the container.
##
```

View containers:

```bash
$ lxc-ls --fancy
NAME   STATE     AUTOSTART   GROUPS   IPV4   IPV6   UNPRIVILIGED
db1    STOPPED   0           -        -      -      false
web1   STOPPED   0           -        -      -      false
web2   STOPPED   0           -        -      -      false
```

Now start the containers:

```bash
$ lxc-start -n db1 -d

$ lxc-start -n web1 -d

$ lxc-start -n web2 -d
```

```bash
$ lxc-ls --fancy
NAME   STATE     AUTOSTART   GROUPS   IPV4         IPV6   UNPRIVILIGED
db1    RUNNING   0           -        10.0.3.167   -      false
web1   RUNNING   0           -        10.0.3.86    -      false
web2   RUNNING   0           -        10.0.3.229   -      false
```

Attach to **db1** i.e. jump onto the instance (where we note the prompt change):

```bash
root@david-virtualBox:~# lxc-attach -n db1
root@db1:~# ls -las
total 16
...
```

Ansible only requires **ssh** (OpenSSH) and **python** installed on a remote machine to be managed.

```bash
root@db1:~# apt-get install python-minimal --no-install-recommends

root@db1:~# python --version
Python 2.7.15rc1
```

```bash
root@david-virtualBox:~# lxc-attach -n web1

root@web1:~# apt-get install python-minimal --no-install-recommends
```

```bash
root@david-virtualBox:~# lxc-attach -n web2

root@web2:~# apt-get install python-minimal --no-install-recommends
```

