# Ansible Playbooks

Create and start a new container:

```bash
$ sudo lxc-create -n playbooks -t ubuntu

$ sudo lxc-start -n playbooks -d
```

```bash
$ sudo lxc-ls -f
NAME   			STATE     AUTOSTART   GROUPS   IPV4         IPV6   UNPRIVILIGED
db1    			RUNNING   0           -        10.0.3.226   -      false
web1   			RUNNING   0           -        10.0.3.88    -      false
web2   			RUNNING   0           -        10.0.3.10    -      false
playbooks 	RUNNING   0           -        10.0.3.210   -      false
```

```bash
$ ssh ubuntu@10.0.3.210
```

Exit and create a new hosts file e.g. **play-hosts** for our new container:

```bash
$ vim play-hosts
```

```properties
10.0.3.210
```

Before we proceed, make sure we have the following installed:

```bash
$ sudo apt-get install sshpass
```

And copy over your public ssh key:

```bash
ssh-copy-id -i ~/.ssh/id_rsa ubuntu@10.0.3.210
```

We have a [playbook](../src/prepare-ansible-target.yml) to *setup* our new container:

To run it:

```bash
$ ansible-playbook prepare-ansible-target.yml -i play-hosts -u ubuntu -k --ask-sudo-pass
...
SSH password: ubuntu
SUDO password[defaults to SSH password]:

PLAY [all] *********************************************************************

TASK [Update Packages] *********************************************************
changed: [10.0.3.210]

TASK [Install Python 2] ********************************************************
changed: [10.0.3.210]

TASK [Fancy way of doing authorized_keys] **************************************
ok: [10.0.3.210]

TASK [COMMON | Set environment] ************************************************
ok: [10.0.3.210]

TASK [COMMON | Generate locales] ***********************************************
skipping: [10.0.3.210]

TASK [COMMON | Reconfigure locales] ********************************************
skipping: [10.0.3.210]

PLAY RECAP *********************************************************************
10.0.3.210                 : ok=4    changed=2    unreachable=0    failed=0
```
