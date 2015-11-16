# System Hostname (`system-hostname`) - Testing

## Overview

To ensure this role works correctly, tests **MUST** be written for any role changes. Roles must pass their tests before 
new versions are released. Manual methods are used to test this role.

These tests, and their different configurations, aim to cover the most frequent, and not all, ways a role is used. 

Three aspects of this role are tested:

1. **Valid role syntax** - as determined by `ansible-playbook --syntax-check`
2. **Functionality** - I.e. does this role do what it claims to 
3. **Idempotency** - I.e. do any changes occur if this role is applied a second time

Tests for these aspects can be split into:

* **Test tasks** - act like unit tests by testing each task to ensure it functions correctly
* **Test playbooks** - act like integration tests by combining tasks in various scenarios

Test tasks mirror the structure of the `tasks` directory within the main role.
A playbook is applied to a number of test VMs to run a number of different scenarios, using host variables.

Playbooks, host variables and other support files are kept in this `tests` directory.

These scenarios are tested *manually*:

1. `test-bare` - Creates a single machine with a FQDN inventory value

Manually run scenarios are run on all Operating Systems this role supports.

## Manual tests

Manual tests are more complete than Continuous Integration, by testing all test scenarios. These tests are therefore 
slower and more time consuming to run than CI tests. The use of Ansible and simple shell scripts aims to reduce this 
effort/complexity as far as is practical.

### Requirements

* Mac OS X or Linux
* [VMware Fusion](http://vmware.com/fusion) `brew cask install vmware-fusion` [1] [2]
* [Vagrant](http://vagrantup.com) `brew cask install vagrant` [1] [2]
* Vagrant plugins:
    * [Vagrant VMware](http://www.vagrantup.com/vmware) `vagrant plugin install vagrant-vmware-fusion`
    * [Host manager](https://github.com/smdahlen/vagrant-hostmanager) `vagrant plugin install vagrant-hostmanager`
* [Git](http://git-scm.com/) `brew install git` [3] [2]
* [Ansible](http://www.ansible.com) `brew install ansible` [3] [2]
* You have a [private key](https://help.github.com/articles/generating-ssh-keys/) `id_rsa`
and [public key](https://help.github.com/articles/generating-ssh-keys/) `id_rsa.pub` in `~/.ssh/`
* You have an entry like [4] in your `~/.ssh/config`

[1] `brew` is a package manager for Mac OS X, see [here](http://brew.sh/) for details.

[2] Although these instructions uses `brew` and `brew cask` these are not required, 
binaries/packages can be installed manually if you wish.

[3] `brew cask` is a package manager for Mac OS X binaries, see [here](http://caskroom.io/) for details.

[4] SSH config entry

```shell
Host *.v.m
    ForwardAgent yes
    User app
    IdentityFile ~/.ssh/id_rsa
    Port 22
```

### Setup

It is assumed you are in the root of this role.

```shell
cd tests
```

VMs are powered by VMware, managed using Vagrant and configured by Ansible.

```shell
$ vagrant up
```

Vagrant will automatically configure the localhost hosts file for infrastructure it creates on your behalf:

| Name                                   | Points To         | FQDN                                        | Notes                       |
| -------------------------------------- | ----------------- | ------------------------------------------- | --------------------------- |
| barc-system-hostname-test--ubuntu-bare | *computed value*  | `barc-system-hostname-test-ubuntu-bare.v.m` | The VM's private IP address |
| barc-system-hostname-test--centos-bare | *computed value*  | `barc-system-hostname-test-centos-bare.v.m` | The VM's private IP address |

Note: Vagrant managed VMs also have a second, host-guest only, network for management purposes not documented here.

### Usage

Use this shell script to run all test phases automatically:

```shell
$ ./tests/run-local-tests.sh
```

Alternatively run each phase separately:

```shell
# Check syntax:
$ ansible-playbook provisioning/site-test.yml --syntax-check

# Apply playbook:
$ ansible-playbook provisioning/site-test.yml

# Apply again to check idempotency:
$ ansible-playbook provisioning/site-test.yml
```

Note: The use of `#` in the above indicates a comment, not a root shell.

### Clean up

```shell
$ vagrant destroy
```
