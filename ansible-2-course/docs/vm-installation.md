# VM Installation

We shall set up a VM using Ubuntu. At the time of writing, we downloaded [Ubuntu 18.04.2 LTS](https://www.ubuntu.com/download/desktop) which corresponds to **ubuntu-18.04.2-desktop-amd64.iso**.

Setup up a VM with Virtualbox. Upon opening Virtualbox:

![VM step 1](images/vm-step-1.png)

---

![VM step 2](images/vm-step-2.png)

---

![VM step 3](images/vm-step-3.png)

---

![VM step 4](images/vm-step-4.png)

---

![VM step 5](images/vm-step-5.png)

---

![VM step 6](images/vm-step-6.png)

---

![VM step 7](images/vm-step-7.png)

It would be a good idea to share this project's **src** with our **virtual machine** (as we'll use this later):

![Select shared folders](images/select-shared-folders.png)

---

![Add shared folder](images/add-shared-folder.png)

---

![Shard folder ok](images/shared-folder-ok.png)

Start our VM using the Ubuntu image we downloaded:

![VM start](images/vm-start.png)

---

![Choose ISO](images/choose-iso.png)

---

![Choose ISO step 2](images/choose-iso-2.png)

---

![Install ubuntu](images/install-ubuntu.png)

---

![Include 3rd party software](images/ubuntu-3rd-party.png)

---

![Scary warning is fine](images/scary-warning-is-fine.png)

---

![Ubuntu user](images/ubuntu-user.png)

For this (noddy) VM setup, we don't actually care about security, so I went for a weak password of **password** and automatic login.

![Sharing](images/sharing.png)

```bash
$ sudo apt-get update

$ sudo apt-get install build-essential gcc make perl dkms

$ reboot
```

Now, select **Devices** from VM menu and **Insert Guest Additions CD image...**

![Devices](images/devices.png)

```bash
$ sudo adduser davidainslie vboxsf
Adding user davidainslie to group vboxsf
```

Reboot the VM. Using **Files** app, navigate to **computer > media > davidainslie**