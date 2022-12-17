Azure Virtual Network Role
=========

Creates, updates and deletes virtual networks in Azure.

Requirements
------------

Requires the [Azure Ansible Collection](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html) be installed.

Role Variables
--------------

This role takes a list named `az_virtual_networks` as input.  
Each item in the list can have parameters set according to the [azure_rm_virtualnetwork module](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/azure_rm_virtualnetwork_module.html) documentation.

For example:

```yaml
az_virtual_networks:
# Creates a virtual network
  - name: "vnet-example1"
    resource_group: "rg-example"
    address_prefixes_cidr:
      - "10.0.0.0/16"
# Deletes a virtual network
  - name: "vnet-example2"
    resource_group: "rg-example"
    state: "absent"
# Full example
  - name: "vnet-example3"
    resource_group: "rg-example"
    location: "australiaeast"
    state: "present"
    tags:
      environment: "production"
      owner: "johndoe@example.com"
    append_tags: true
    address_prefixes_cidr:
      - "10.0.0.0/16"
    purge_address_prefixes: false
    dns_servers:
      - "1.1.1.1"
      - "1.0.0.1"
    purge_dns_servers: false
```

Example Playbook
----------------

```yaml
---
- hosts: localhost
  connection: local
  roles:
    - az_virtualnetwork
```
