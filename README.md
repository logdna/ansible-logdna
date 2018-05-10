# Deploy LogDNA Agent with Ansible

## Description
Ansible Galaxy Role to install and configure LogDNA Agent

## Requirements
* Ansible version: `>=2.1`
* Tested on the following Operating Systems:
    * CentOS 6
    * CentOS 7
    * Ubuntu 12.04 - Precise
    * Ubuntu 14.04 - Trusty
    * Ubuntu 16.04 - Xenial
    * Ubuntu 17.10 - Artful
    * Debian 8 - Jessie

## Role Variables
### Task-specific Variables
* `agent_install`: `true` if to be installed (default: `true`)
* `agent_config`: `true` if to be configured (default: `true`)
* `agent_service`: (default: `started`), supporting:
    * `started`: to start LogDNA Agent Service if `conf_key` is specified
    * `restarted`: to restart LogDNA Agent Service
    * `stopped`: to stop LogDNA Agent Service.

### Configuration Variables
These variables map directly to the native configuration options for the LogDNA Agent:
* `conf_key`: LogDNA Ingestion Key - LogDNA Agent service will not start if `conf_key` is not specified
* `conf_config`: File Path for the LogDNA Agent configuration (defaults to `/etc/logdna.conf`)
* `conf_logdir`: Log Directories to be added
* `conf_logfile`: Log Files to be added
* `conf_exclude`: Log Files or Directories to be excluded
* `conf_exclude_regex`: Exclusion Rule for Log Lines
* `conf_hostname`: Alternative host name to be used
* `conf_tags`: Tags to be added.

## How to Install:
* Online from Ansible Galaxy: `ansible-galaxy install logdna.logdna`
* Directly from Source Code: `ansible-galaxy install git+https://github.com/logdna/ansible-logdna.git`

## Example Playbook
```bash
- hosts: <hosts>
  vars:
    conf_key: <LogDNA Ingestion Key>
  roles:
     - { role: logdna.logdna }
```

## Use Cases
* To install, configure, and start the service on specified hosts:
```bash
- hosts: <hosts>
  vars:
    conf_key: <LogDNA Ingestion Key>
    # All other configuration parameter specifications
  roles:
     - { role: logdna.logdna }
```
* To reconfigure and restart the service on specified hosts:
```bash
- hosts: <hosts>
  vars:
    # reconfiguration parameter specifications
    agent_service: restarted
  roles:
     - { role: logdna.logdna }
```
* Just install but don't configure or touch the service:
```bash
- hosts: <hosts>
  vars:
    # do not set LogDNA Ingestion Key
    agent_config: false
  roles:
     - { role: logdna.logdna }
```
* Stop the service:
```bash
- hosts: <hosts>
  vars:
    agent_install: false
    agent_config: false
    agent_service: stopped
  roles:
     - { role: logdna.logdna }
```

## License and Authors

* Author: [Samir Musali](https://github.com/ldsamir), LogDNA
* License: MIT
