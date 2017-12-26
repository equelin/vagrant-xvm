# vagrant-xvm

This Vagrantfile purpose is to quickly setup an Ubuntu box with the VMware Cross vCenter Workload Migration Utility installed.

### Prerequisites

- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/) (or other tool compatible with vagrant)
- [Cross vCenter Workload Migration Utility](https://labs.vmware.com/flings/cross-vcenter-workload-migration-utility#summary)

### Usage

1. Download or clone this repository
2. Extract the utility and put it in the Vagrant folder (default folder name is `xvm`. Can be tweaked if needed. See point 3). The folder tree should looks like this:

```Bash
├───xvm
│   └xvm-1.0.jar
├─.gitignore
├─LICENSE
├─README.md
├─Vagrantfile
```

3. Change the variables in the `Vagrantfile` according to your needs

```Ruby
## Infrastructure
$box_image = "ubuntu/xenial64"

## XVM folder and file names
$xvm_folder = "./xvm"
$xvm_jar = "xvm-1.0.jar"

## XVM port
$xvm_port = 8080
```

4. Launch the VM build with the command `vagrant up`

```Bash
> vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'ubuntu/xenial64'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'ubuntu/xenial64' is up to date...
==> default: Setting the name of the VM: vagrant-xvm_default_1508399698618_92030
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 8080 (guest) => 8080 (host) (adapter 1)
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
...
```

5. Check that everything goes well by connecting to the web interface at the url `http://localhost:8080` (modify the port according to your setup)
6. Migrate your VM !

# Author

**Erwan Quélin**
- <https://github.com/equelin>
- <https://twitter.com/erwanquelin>

# License

Copyright 2017 Erwan Quelin and the community.

Licensed under Apache License Version 2.0.