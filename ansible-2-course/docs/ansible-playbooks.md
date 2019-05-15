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

