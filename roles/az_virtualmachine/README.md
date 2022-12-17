Azure Virtual Machine Role
=========

Creates, updates and deletes virtual machines in Azure.

Requirements
------------

Requires the [Azure Ansible Collection](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html) be installed.

Role Variables
--------------

This role takes a list named `az_virtual_machines` as input.  
Each item in the list can have parameters set according to the [azure_rm_virtualmachine module](https://docs.ansible.com/ansible/latest/collections/azure/azcollection/azure_rm_virtualmachine_module.html) documentation.

For example:

```yaml
az_virtual_machines:
# Creates a virtual machine
  - name: "vm-example1"
    resource_group: "rg-example"
# Deletes a virtual machine
  - name: "vm-example2"
    resource_group: "rg-example"
    state: "absent"
# Full example
  - name: "vm-example3"
    resource_group: "rg-example"
    state: "present"
    tags:
      environment: "production"
      owner: "johndoe@example.com"
    append_tags: true
    accept_terms: false
    admin_username: "azureuser"
    admin_password: "SUPERSECUREPASSWORD"
    allocated: true
    availability_set: "avail-example1"
    boot_diagnostics:
      enabled: true
      resource_group: "rg-example"
      storage_account: "stvm-example1"
    custom_data: |
      #cloud-config
      packages_update: true
      packages_upgrade: true
      packages:
        - bash-completion
        - vim
    data_disks:
      - caching: "ReadOnly"
        disk_size_gb: "64"
        lun: 0
        managed_disk_type: "Standard_LRS"
        storage_account_name: "stvm-example2"
        storage_blob_name: "vm-example3date20220820lun0.vhd"
        storage_container_name: "vhds"
    ephemeral_os_disk: false
    eviction_policy: "Deallocate"
    generalized: false
    image:
      publisher: "erockyenterprisesoftwarefoundationinc1653071250513"
      offer: "rockylinux-9"
      sku: "rockylinux-9"
      version: "latest"
    license_type: "None"
    managed_disk_type: "Standard_LRS"
    max_price: -1
    network_interface_names:
      - "nic-example1"
    open_ports:
      - 22
    os_disk_name: "osdisk-example1"
    os_disk_size_gb: "20"
    os_type: "Linux"
    plan: "{{ omit }}"
    priority: "Spot"
    public_ip_allocation_method: "Static"
    remove_on_absent:
      - "all"
    restarted: false
    short_hostname: "vm-example3"
    ssh_password_enabled: true
    ssh_public_keys: "{{ omit }}"
    started: true
    storage_account_name: "stvm-example01"
    storage_blob_name: "vm-example3.vhd"
    storage_container_name: "vhds"
    subnet_name: "snet-example1"
    virtual_network_name: "vnet-example1"
    virtual_network_resource_group: "rg-example1"
    vm_size: "Standard_D4"
    zones:
      - 1
```

Example Playbook
----------------

```yaml
---
- hosts: localhost
  connection: local
  roles:
    - az_virtualmachine
```
