Azure Network Interface Role
=========

Creates, updates and deletes network interfaces in Azure.

Requirements
------------

Requires the [Azure Ansible Collection](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html) be installed.

Role Variables
--------------

This role takes a list named `az_network_interfaces` as input.  
Each item in the list can have parameters set according to the [azure_rm_networkinterface module](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/azure_rm_networkinterface_module.html) documentation.

For example:

```yaml
az_network_interfaces:
# Creates a network interface
  - name: "nic-example1"
    resource_group: "rg-example"
    virtual_network: "vnet-example1"
    subnet_name: "snet-example1"
    ip_configurations:
      - name: "ipc-example1"
        primary: true
        public_ip_address_name: "pip-example1"
    security_group: "nsg-example1"
# Deletes a network interface
  - name: "nic-example2"
    resource_group: "rg-example"
    virtual_network: "vnet-example2"
    subnet_name: "snet-example2"
    state: "absent"
# Full example
  - name: "nic-example3"
    resource_group: "rg-example"
    virtual_network: "vnet-example3"
    subnet_name: "snet-example3"
    location: "australiaeast"
    state: "present"
    tags:
      environment: "production"
      owner: "johndoe@example.com"
    append_tags: true
    create_with_security_group: true
    dns_servers:
      - "1.1.1.1"
      - "1.0.0.1"
    enable_accelerated_networking: false
    enable_ip_forwarding: false
    ip_configurations:
      - name: "ipc-example3"
        primary: true
        public_ip_address_name: "pip-example3"
        load_balancer_backend_address_pools:
          - load_balancer: "lbe-example1"
            name: "bap-example1"
    open_ports:
      - 22
      - 3389
    os_type: "Linux"
    security_group: "nsg-example3"
```

Example Playbook
----------------

```yaml
---
- hosts: localhost
  connection: local
  roles:
    - az_networkinterface
```
