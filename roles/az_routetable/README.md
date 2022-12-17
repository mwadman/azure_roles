Azure Route Table Role
=========

Creates, updates and deletes route tables in Azure.

Requirements
------------

Requires the [Azure Ansible Collection](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html) be installed.

Role Variables
--------------

This role takes a list named `az_route_tables` as input.  
Each item in the list can have parameters set according to the [azure_rm_routetable module](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/azure_rm_routetable_module.html) documentation.

For example:

```yaml
az_route_tables:
# Creates a route table
  - name: "rt-example1"
    resource_group: "rg-example"
# Deletes a route table
  - name: "rt-example2"
    resource_group: "rg-example"
    state: "absent"
# Full example
  - name: "rt-example3"
    resource_group: "rg-example"
    location: "australiaeast"
    state: "present"
    tags:
      environment: "production"
      owner: "johndoe@example.com"
    append_tags: true
    disable_bgp_route_propagation: false
```

Example Playbook
----------------

```yaml
---
- hosts: localhost
  connection: local
  roles:
    - az_routetable
```
