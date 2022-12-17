Azure Load Balancer Role
=========

Creates, updates and deletes load balancers in Azure.

Requirements
------------

Requires the [Azure Ansible Collection](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html) be installed.

Role Variables
--------------

This role takes a list named `az_load_balancers` as input.  
Each item in the list can have parameters set according to the [azure_rm_loadbalancer module](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/azure_rm_loadbalancer_module.html) documentation.

For example:

```yaml
az_load_balancers:
# Creates a load balancer
  - name: "lbe-example1"
    resource_group: "rg-example"
    backend_address_pools:
      - name: "bap-example1"
    frontend_ip_configurations:
      - name: "fic-example1"
        public_ip_address: "pip-example1"
    load_balancing_rules:
      - name: "rule-example1"
        backend_address_pool: "bap-example1"
        backend_port: 443
        frontend_ip_configuration: "fic-example1"
        frontend_port: 443
        load_distribution: "Default"
        probe: "hp-example1"
        protocol: "Tcp"
    probes:
      - name: "hp-example1"
        fail_count: 3
        interval: 15
        port: 443
        protocol: "Http"
        request_path: "/health"
# Deletes a load balancer
  - name: "lbe-example2"
    resource_group: "rg-example"
    state: "absent"
# Full example
  - name: "lbe-example3"
    resource_group: "rg-example"
    location: "australiaeast"
    state: "present"
    tags:
      environment: "production"
      owner: "johndoe@example.com"
    append_tags: true
    backend_address_pools:
      - name: "bap-example3"
    frontend_ip_configurations:
      - name: "fic-example3"
        public_ip_address: "pip-example3"
    inbound_nat_pools:
      - name: "inp-example3"
        frontend_ip_configuration_name: "fic-example3"
        protocol: "Tcp"
        frontend_port_range_start: 80
        frontend_port_range_end: 81
        backend_port: 443
    inbound_nat_rules:
      - name: "inr-example3"
        backend_port: 443
        protocol: Tcp
        frontend_port: 443
        frontend_ip_configuration: "fic-example3"
    load_balancing_rules:
      - name: "rule-example3"
        backend_address_pool: "bap-example3"
        backend_port: 443
        frontend_ip_configuration: "fic-example3"
        frontend_port: 443
        load_distribution: "Default"
        probe: "hp-example3"
        protocol: "Tcp"
    probes:
      - name: "hp-example3"
        fail_count: 3
        interval: 15
        port: 443
        protocol: "Http"
        request_path: "/health"
    sku: "Standard"
```

Example Playbook
----------------

```yaml
---
- hosts: localhost
  connection: local
  roles:
    - az_loadbalancer
```
