Role Name
=========

The ansible role deploys and configures all services for an Ophidia cluster

Introduction
------------

The repository contains ansible-roles that are published in
ansible galaxy: https://galaxy.ansible.com/indigo-dc/ophidia-cluster/

Requirements
------------

No additional requirements

Role Variables
--------------

Default role varibles are:

1. oph_user: user that will run the framework
2. cert_passwd: the password for the certificates, user account and mysql

Dependencies
------------

None

Example Playbook
----------------


An example of playbook to deploy Ophidia:

```
---
- hosts: localhost
  roles:
    - { role: indigo-dc.ophidia-cluster }
```

Or execute:

```
$ ansible-playbook /etc/ansible/roles/indigo-dc.ophidia-cluster/tests/test.yml
```

Further documentation
---------------------

* Ophidia: http://ophidia.cmcc.it/documentation/
* Installation and configuration: http://ophidia.cmcc.it/documentation/admin/index.html

License
-------

Apache v2


Author information
------------------

ophidia-info@lists.cmcc.it

