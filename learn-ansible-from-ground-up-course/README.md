# Learn Ansible from Ground Up Course

In the (pre) [setup](../docs/setup.md) we install Ansible using Homebrew - Very simple.

However, we can also work with virtual machines managed by Vagrant (again installed with Homebrew) and then follow along with installing Ansible within a VM.

## Centos

```bash
$ mkdir ansible-machines
$ cd ansible-machines

$ vagrant init bento/centos-7.3

$ ls -las
8 -rw-r--r--  1 davidainslie  staff  3023 21 Nov 15:06 Vagrantfile

$ vargrant up

$ vargrant ssh
```

```basic
[vagrant@localhost ~]$ df -h
Filesystem           Size  Used Avail Use% Mounted on
/dev/mapper/cl-root   37G  1.2G   36G   4% /
devtmpfs             487M     0  487M   0% /dev
tmpfs                497M     0  497M   0% /dev/shm
tmpfs                497M  6.5M  490M   2% /run
tmpfs                497M     0  497M   0% /sys/fs/cgroup
/dev/sda1           1014M  183M  832M  18% /boot
vagrant              932G  731G  202G  79% /vagrant
tmpfs                100M     0  100M   0% /run/user/1000

[vagrant@localhost ~]$ ifconfig -a
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
        inet6 fe80::2d36:6f15:e1e2:fdaf  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:37:f8:46  txqueuelen 1000  (Ethernet)
        RX packets 1123  bytes 110412 (107.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 859  bytes 100122 (97.7 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 12  bytes 1020 (1020.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 12  bytes 1020 (1020.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

[vagrant@localhost ~]$ exit
logout
Connection to 127.0.0.1 closed
```

```bash
$ vagrant destroy
```

```bash
$ vim Vagrantfile
```

and add the following:

```ruby
config.vm.define "client" do | client |
  client.vm.hostname = "client"
end
```

which creates a machine named "client" in the current directory - let's see:

```bash
$ vagrant up
$ vagrant ssh
```

```basic
[vagrant@client ~]$
```

Note the **@client** now instead of **@localhost**.

```basic
[vagrant@client ~]$ sudo rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

[vagrant@client ~]$ ls -l /etc/yum.repos.d
total 36
-rw-r--r--. 1 root root 1664 Nov 29  2016 CentOS-Base.repo
-rw-r--r--. 1 root root 1309 Nov 29  2016 CentOS-CR.repo
-rw-r--r--. 1 root root  649 Nov 29  2016 CentOS-Debuginfo.repo
-rw-r--r--. 1 root root  314 Nov 29  2016 CentOS-fasttrack.repo
-rw-r--r--. 1 root root  630 Nov 29  2016 CentOS-Media.repo
-rw-r--r--. 1 root root 1331 Nov 29  2016 CentOS-Sources.repo
-rw-r--r--. 1 root root 2893 Nov 29  2016 CentOS-Vault.repo
-rw-r--r--. 1 root root  951 Oct  2  2017 epel.repo
-rw-r--r--. 1 root root 1050 Oct  2  2017 epel-testing.repo

[vagrant@client ~]$ sudo yum -y install ansible

[vagrant@client ~]$ ansible --version
ansible 2.7.2
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/vagrant/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.5 (default, Nov  6 2016, 00:28:07) [GCC 4.8.5 20150623 (Red Hat 4.8.5-11)]
```

# Ubuntu

The above was done for **centos-7.3**. However, we could just as easily have done it for **ubuntu** again within the root (of this course) directory:

```bash
$ mkdir ubuntu
$ cd ubuntu
$ vagrant init bento/ubuntu-18.04
$ vagrant up
$ vagrant ssh
```

```basic
vagrant@vagrant:~$ sudo apt-add-repository ppa:ansible/ansible

vagrant@vagrant:~$ sudo apt-get update
  
vagrant@vagrant:~$ sudo apt-get install ansible
    
vagrant@vagrant:~$ ansible --version
ansible 2.7.2
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/vagrant/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.15rc1 (default, Apr 15 2018, 21:51:34) [GCC 7.3.0]    
```

