Azure Subnet Role
=========

Creates, updates and deletes subnets in Azure.

Requirements
------------

Requires the [Azure Ansible Collection](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html) be installed.

Role Variables
--------------

This role takes a list named `az_subnets` as input.  
Each item in the list can have parameters set according to the [azure_rm_subnet module](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/azure_rm_subnet_module.html) documentation.

For example:

```yaml
az_subnets:
# Creates a subnet
  - name: "snet-example1"
    resource_group: "rg-example"
    virtual_network_name: "vnet-example1"
# Deletes a subnet
  - name: "snet-example2"
    resource_group: "rg-example"
    virtual_network_name: "vnet-example2"
    state: "absent"
# Full example
  - name: "snet-example3"
    resource_group: "rg-example"
    virtual_network_name: "vnet-example3"
    state: "present"
    address_prefix_cidr: "192.168.0.0/24"
    delegations:
      - name: "del-example3"
        serviceName: "Microsoft.ContainerInstance/containerGroups"
    private_endpoint_network_policies: "Enabled"
    private_link_service_network_policies: "Enabled"
    route_table: "rt-example3"
    security_group: "sg-example3"
    service_endpoints:
      - service: "Microsoft.Sql"
```

Example Playbook
----------------

```yaml
---
- hosts: localhost
  connection: local
  roles:
    - az_subnet
```
