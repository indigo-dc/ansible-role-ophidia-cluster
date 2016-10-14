Role Name
=========

The ansible role deploys and configures all services for an Ophidia cluster. 

Introduction
------------

The repository contains ansible-roles that are published in
ansible galaxy: https://galaxy.ansible.com/indigo-dc/ophidia-cluster/

Requirements
------------

No additional requirements

Role Variables
--------------

Role variables for Ophidia cluster are:

1. cert_passwd: the password for the certificates and user account
2. ophdb_passwd: the password for MySQL
3. oph_user: user that will run the framework
4. base_path: base path for data
5. server_ip: Ophidia server ip address
6. compute_subnet: subnetwork for Ophidia io-compute nodes
7. mysql_subnet: subnetwork for Ophidia io-compute nodes (for database grant)
8. deploy_type: type of deployment ('install' or 'configure')
9. slurm_nodes_name: prefix for io-compute nodes
10. slurm_nodes_ips: list of IPs of io-compute nodes
11. node_type: type of node ('server' or 'io')

Dependencies
------------

It requires indigo-dc.nfs ansible role.

Example Playbook
----------------

An example of playbook to install an Ophidia cluster:

```
---
- hosts: oph-server
  roles:
    - {role: 'indigo-dc.ophidia-cluster', node_type: 'server', deploy_type: 'install'}

- hosts: oph-io
  roles:
    - {role: 'indigo-dc.ophidia-cluster', node_type: 'io', deploy_type: 'install'}

```

An example of playbook to configure an Ophidia cluster:

```
---
- hosts: oph-server
  roles:
    - {role: 'indigo-dc.ophidia-cluster', node_type: 'server', deploy_type: 'configure', slurm_nodes_ips: "{{ groups['oph-io']|map('extract', hostvars, 'ansible_default_ipv4')|list }}", mysql_subnet: "{{ ansible_default_ipv4.network }}/{{ ansible_default_ipv4.netmask }}", compute_subnet: "{{ ansible_default_ipv4.network }}/24", server_ip: '{{ ansible_default_ipv4.address }}'}

- hosts: oph-io
  roles:
    - {role: 'indigo-dc.ophidia-cluster', node_type: 'io', deploy_type: 'configure', mysql_subnet: "{{ ansible_default_ipv4.network }}/{{ ansible_default_ipv4.netmask }}", server_ip: "{{hostvars['oph-server']['ansible_default_ipv4']}}"}

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

