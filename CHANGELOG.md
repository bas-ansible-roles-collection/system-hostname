# System Hostname (`system-hostname`) - Change log

All notable changes to this role will be documented in this file.
This role adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

Note: Developers - make sure to set the `BARC_role_version` variable when releasing new versions of this role.

## [Unreleased][unreleased]

### Added

* Note to explain why testing dependencies do not include meta-roles this role is a part of
* Local facts to record this role has been applied to a system and its version, plus supporting documentation sections

### Fixed

* Incorrect group variable for BARC role name
* README formatting and typos
* Minor corrections to other files for formatting and typos
* Testing role dependencies should always use latest versions

### Changed

* Migrating from old Ansible Galaxy namespace, 'BARC', to 'bas-ansible-roles-collection'
* Migrating from old Ansible Galaxy 'categories' to new 'tags' meta-data
* Migrating from old Repository in 'antarctica' to 'bas-ansible-roles-collection'

### Removed

* Unnecessary CI testing playbook, as CI is not used for this role yet

## 0.1.1 - 19/11/2015

### Added

* Git attributes file to produce cleaner release archives and improve language stats on GitHub

### Fixed

* `.gitignore` patterns for keeping the roles/BARC.prelude/meta/main.yml file
* Erroneous change events for testing tasks

### Changed

* Updating role dependencies for testing
* Improved comments for provisioning playbooks
* Updating testing provisioning to latest conventions

## 0.1.0 - 16/11/2015

### Added

* Initial version - with support for setting the hostname and FQDN of a machine
