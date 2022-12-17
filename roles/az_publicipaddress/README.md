Azure Public IP Address Role
=========

Creates, updates and deletes public ip addresses in Azure.

Requirements
------------

Requires the [Azure Ansible Collection](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html) be installed.

Role Variables
--------------

This role takes a list named `az_public_ips` as input.  
Each item in the list can have parameters set according to the [azure_rm_publicipaddress module](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/azure_rm_publicipaddress_module.html) documentation.

For example:

```yaml
az_public_ips:
# Creates a Public IP Address
  - name: "pip-example1"
    resource_group: "rg-example"
# Deletes a Public IP Address
  - name: "pip-example2"
    resource_group: "rg-example"
    state: "absent"
# Full example
  - name: "pip-example3"
    resource_group: "rg-example"
    location: "australiaeast"
    state: "present"
    tags:
      environment: "production"
      owner: "johndoe@example.com"
    append_tags: false
    allocation_method: "static"
    domain_name: "example3"
    idle_timeout: 4
    ip_tags:
      - type: "RoutingPreference"
        value: "Internet"
    sku: "standard"
    version: "ipv4"
```

Example Playbook
----------------

```yaml
---
- hosts: localhost
  connection: local
  roles:
    - az_publicipaddress
```
