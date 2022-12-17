Azure Security Group Role
=========

Creates, updates and deletes security groups in Azure.

Requirements
------------

Requires the [Azure Ansible Collection](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html) be installed.

Role Variables
--------------

This role takes a list named `az_network_security_groups` as input.  
Each item in the list can have parameters set according to the [azure_rm_securitygroup module](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/azure_rm_securitygroup_module.html) documentation.

For example:

```yaml
az_network_security_groups:
# Creates a security group
  - name: "nsg-example1"
    resource_group: "rg-example"
# Deletes a security group
  - name: "nsg-example2"
    resource_group: "rg-example"
    state: "absent"
# Add custom rules
  - name: "nsg-example3"
    resource_group: "rg-example"
    rules:
      - name: "Allow HTTPS to Load Balancer"
        priority: "1001"
        access: "Allow"
        direction: "Inbound"
        protocol: "Tcp"
        source_address_prefix: "*"
        source_port_range: "*"
        destination_address_prefix: "AzureLoadBalancer"
        destination_port_range: "443"
# Full example
  - name: "nsg-example4"
    resource_group: "rg-example"
    location: "australiaeast"
    state: "present"
    tags:
      environment: "production"
      owner: "johndoe@example.com"
    append_tags: true
    default_rules:
      - name: "AllowVnetInBound"
        priority: "65000"
        access: "Allow"
        direction: "Inbound"
        source_address_prefix: "VirtualNetwork"
        destination_address_prefix: "VirtualNetwork"
      - name: "AllowAzureLoadBalancerInBound"
        priority: "65001"
        access: "Allow"
        direction: "Inbound"
        source_address_prefix: "AzureLoadBalancer"
      - name: "DenyAllInBound"
        priority: "65500"
        access: "Deny"
        direction: "Inbound"
      - name: "AllowVnetOutBound"
        priority: "65000"
        access: "Allow"
        direction: "Outbound"
        source_address_prefix: "VirtualNetwork"
        destination_address_prefix: "VirtualNetwork"
      - name: "AllowInternetOutBound"
        priority: "65001"
        access: "Allow"
        direction: "Outbound"
        destination_address_prefix: "Internet"
      - name: "DenyAllOutBound"
        priority: "65500"
        access: "Deny"
        direction: "Outbound"
    purge_default_rules: false
    rules:
      - name: "ICMP"
        protocol: "Icmp"
        priority: "1001"
    purge_rules: false
```

Example Playbook
----------------

```yaml
---
- hosts: localhost
  connection: local
  roles:
    - az_securitygroup
```
