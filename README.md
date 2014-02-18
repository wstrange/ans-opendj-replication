opendj-replication
========

[Ansible](http://www.ansible.com) role to setup replication between two [OpenDJ](http://opendj.forgerock.org/) LDAP v3 servers.

Assumes the two instances have already been installed.

The "primary" instance initiates replication with a secondary instance. 

Requirements
------------

Requires Java SDK (1.7 or later) installed on the target.


Role Variables
--------------

Default Variables (see defaults/main.yml for a complete list)

- install_root (/opt). Where primary OpenDJ is installed on the guest
- opendj_admin_port (4444). Admin port for primary instance
- opendj_admin_port2 (1444). Admin port for secondary instance
- opendj_basedn (dc=example,dc=com).  The default base DN to replicate
- opendj_password (password) Default admin password for OpenDJ 
- opendj_password2 (password) Default admin password for second OpenDJ instance 
- opendj_replication_port ( 8989). Replication port for primary
- opendj_replication_port2 ( 8990). Replication port for second instance. Defaults to
a different port so we can replicate two instances on the same host.



Example
-------

Configure two instances of OpenDJ on the same server (different ports) and replicate
between them. The primary server uses default ports, passwords, etc.

    - hosts: ldap
      roles:
          - { role: opendj, install_root: "/opt/a" }
          - { role: opendj, install_root: "/opt/b", opendj_admin_port: 1444, opendj_ldap_port: 2389,
              opendj_ldaps_port: 2636 , opendj_jmx_port: 2689, opendj_service_name: "opendj2" }
          - { role: opendj-replication, install_root: "/opt/a", opendj_host2: localhost, 
                    opendj_admin_port2: 1444 }


Dependencies
------------

opendj role 


License
-------

MIT

Author Information
------------------

Warren Strange. 

