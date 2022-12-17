Azure Resource Group Role
=========

Creates and deletes resource groups in Azure.

Requirements
------------

Requires the [Azure Ansible Collection](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html) be installed.

Role Variables
--------------

This role takes a list named `az_resource_groups` as input.  
Each item in the list can have parameters set according to the [azure_rm_resourcegroup module](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/azure_rm_resourcegroup_module.html) documentation.

For example:

```yaml
az_resource_groups:
# Creates a resource group
  - name: "rg-example1"
    location: "australiaeast"
# Deletes a resource group
  - name: "rg-example2"
    location: "australiaeast"
    state: "absent"
# Deletes a resource group even if resources are present
  - name: "rg-example3"
    location: "australiaeast"
    state: "absent"
    force_delete_nonempty: "yes"
# Full example
  - name: "rg-example4"
    location: "australiaeast"
    state: "present"
    tags:
      environment: "production"
      owner: "johndoe@example.com"
    append_tags: "yes"
    force_delete_nonempty: "no"
```

Example Playbook
----------------

To create a resource group

```yaml
---
- hosts: localhost
  connection: local
  roles:
    - az_resourcegroup
```
