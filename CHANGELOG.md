# System Hostname (`system-hostname`) - Change log

All notable changes to this role will be documented in this file.
This role adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [Unreleased][unreleased]

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
