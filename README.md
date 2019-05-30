freebsd-jailed
=========

[![Build Status](https://travis-ci.org/JoergFiedler/freebsd-jailed.svg?branch=master)](https://travis-ci.org/JoergFiedler/freebsd-jailed)

This role just creates a jail. Nothing more. Is used by other roles to create
jailed services. 

Requirements
------------

This role is intent to be used with a fresh FreeBSD installation. There is a
Vagrant Box (https://app.vagrantup.com/JoergFiedler) for your convenience with
providers for VirtualBox and EC2 you may use.

Role Variables
--------------

##### jail_name

The name for the jail. Local part of the hostname. Default: `'{{ jail_net_ip }}'`.

##### jail_domain

Domain part of the hostname. Default: `'darkcity'`.

##### jail_backup_old_files

Set to `yes` if you want to create backup file for file modifications done by Ansible. Default: `no`.

##### jail_freebsd_release

The FreeBSD distribution to use for this jail, e.g. `11.2-RELEASE`. Default: Not
set. `

##### jail_net_if

The interface to which the jail's ip address is added. Default: `'lo0'`.

##### jail_net_ip

The jail's ip address. No default value.

##### jail_net_resolver

The DNS server that will be used as a resolver. If set to `none` resolver 
config from jail host apply to the jails. Default: `none`.

##### jail_use_syslogd_server
##### jail_syslogd_server

The syslogd server to which all syslog messages are going to be forwarded. If
not set messages stay with local syslog. No default value.

This feature is only active if the variable `jail_use_syslogd_server` is set.

##### jail_build_server_enabled

Use own build server repository to install customized build ports. Default: `no`

##### jail_build_server_url

The build server repo http url. Default: `''`

##### jail_build_server_pubkey

The public key to use to verify signatures. Default: `'poudriere.pub'`

Dependencies
------------

- [JoergFiedler.freebsd-jail-host](https://galaxy.ansible.com/JoergFiedler/freebsd-jail-host)

Example Playbook
----------------

	  - hosts: all
        become: true
      
        vars:
          ansible_python_interpreter: '/usr/local/bin/python2.7'
      
        tasks:
          - import_role:
                name: 'JoergFiedler.freebsd-jail-host'
          - import_role:
              name: 'JoergFiedler.freebsd-jailed'
            vars:
              jail_net_ip: '10.1.0.10'
              jail_name: 'jailed'
              jail_freebsd_release: '11.2-RELEASE'

License
-------

BSD

Author Information
------------------

If you like it or do have ideas to improve this project, please open an issue on Github. Thanks.
