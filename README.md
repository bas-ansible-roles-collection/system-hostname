# System Hostname (`system-hostname`)

Configures the hostname and FQDN of a machine

**Part of the BAS Ansible Role Collection (BARC)**

## Overview

* Using the Ansible inventory hostname, sets the current hostname of the machine (i.e. lasts until rebooting)
* Using the Ansible inventory hostname, sets the permanent hostname of the machine (i.e. used after rebooting)
* Using the Ansible inventory hostname, sets the Fully Qualified Domain Name of the machine, for the IPv4 interface
* Using the Ansible inventory hostname, sets the Fully Qualified Domain Name of the machine, for the IPv4 interface

## Quality Assurance

This role uses manual testing to ensure the features offered by this role work as advertised. 
See `tests/README.md` for more information.

## Dependencies

* None

## Requirements

* An Ansible inventory **SHOULD** correctly define the FQDN of each machine to be configured by this role [1].

E.g.

```
# This is an Ansible inventory file.

[group]
machine-1.net.example.com
```

[1] Where only a hostname is defined (e.g. `machine-1`), no FQDN will be set by this role, the hostname still will.

## Limitations

* None

## Usage

### BARC manifest

By default, BARC roles will record that they have been applied to a system. This is recorded using a set of 
[Ansible local facts](http://docs.ansible.com/ansible/playbooks_variables.html#local-facts-facts-d), specifically:

* `ansible_local.barc-nginx.general.role_applied` - to indicate that this role has been applied to a system
* `ansible_local.barc-nginx.general.role_version` - to indicate the version of this this role that has been applied

Note: You **SHOULD** use this feature to determine whether this role has been applied to a system.

If you do not want these facts to be set by this role, you **MUST** skip the **BARC_SET_MANIFEST** tag. No support is 
offered in this case, as other roles or use-cases may rely on this feature. Therefore you **SHOULD** not disable this
feature.

### Typical playbook

Note: It is assumed you have already created a suitable inventory file.

```yaml
---

- name: configure system hostname
  hosts: all
  become: yes
  vars: []
  roles:
    - bas-ansible-roles-collection.system-hostname
```

### Tags

BARC roles use standardised tags to control which aspects of an environment are changed by roles. Where relevant, tags
will be applied at a role, or task(s) level, as indicated below.

This role uses the following tags, for all tasks:

* [**BARC_CONFIGURE**](https://antarctica.hackpad.com/BARC-Standardised-Tags-AviQxxiBa3y#:h=BARC_CONFIGURE)
* [**BARC_CONFIGURE_SYSTEM**](https://antarctica.hackpad.com/BARC-Standardised-Tags-AviQxxiBa3y#:h=BARC_CONFIGURE_SYSTEM)
* [**BARC_CONFIGURE_NETWORKING**](https://antarctica.hackpad.com/BARC-Standardised-Tags-AviQxxiBa3y#:h=BARC_CONFIGURE_NETWORK)
* [**BARC_SET_MANIFEST**](https://antarctica.hackpad.com/BARC-Standardised-Tags-AviQxxiBa3y#:h=BARC_SET_MANIFEST)

### Variables

#### *BARC_role_name*

* **MUST NOT** be specified
* Specifies the name of this role within the BAS Ansible Roles Collection (BARC) used for setting local facts
* See the *BARC roles manifest* section for more information
* Example: system-hostname

#### *BARC_role_version*

* **MUST NOT** be specified
* Specifies the name of this role within the BAS Ansible Roles Collection (BARC) used for setting local facts
* See the *BARC roles manifest* section for more information
* Example: 2.0.0

## Developing

### Issue tracking

Issues, bugs, improvements, questions, suggestions and other tasks related to this package are managed through the 
[BAS Ansible Roles Collection](https://jira.ceh.ac.uk/projects/BARC) (BARC) project on Jira.

This service is currently only available to BAS or NERC staff, although external collaborators can be added on request.
See our contributing policy for more information.

### Source code

All changes should be committed, via pull request, to the canonical repository, which for this project is:

`git clone ssh://git@stash.ceh.ac.uk:7999/barc/system-hostname.git`

A mirror of this repository is maintained on GitHub. Changes are automatically pushed from the canonical repository to
this mirror, in a one-way process.

`git@github.com:bas-ansible-roles-collection/system-hostname.git`

Note: The canonical repository is only accessible within the NERC firewall. External collaborators, please make pull 
requests against the mirrored GitHub repository and these will be merged as appropriate.

### Contributing policy

This project welcomes contributions, see `CONTRIBUTING.md` for our general policy.

The [Git flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow/) 
workflow is used to manage the development of this project:

* Discrete changes should be made within feature branches, created from and merged back into develop 
(where small changes may be made directly)
* When ready to release a set of features/changes, create a release branch from develop, update documentation as 
required and merge into master with a tagged, semantic version (e.g. v1.2.3)
* After each release, the master branch should be merged with develop to restart the process
* High impact bugs can be addressed in hotfix branches, created from and merged into master (then develop) directly

### Release procedure

See [here](https://antarctica.hackpad.com/BARC-Overview-and-Policies-SzcHzHvitkt#:h=Release-procedures) for general 
release procedures for BARC roles.

## Acknowledgements

This role is heavily based on the [ANXS.hostname](https://github.com/ANXS/hostname) role.

## Licence

Copyright 2015 NERC BAS.

Unless stated otherwise, all documentation is licensed under the Open Government License - version 3. All code is
licensed under the MIT license.

Copies of these licenses are included within this role.
