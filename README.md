# Ansible Role: az_create_resource_group

Creates an Azure Resource Group. This role has been made specifically to be used in CI/CD pipelines, hence the usage of a vault file.

## Requirements

Azure.azure_preview_modules

## Role Variables

Variables can be set in the vars/vars.yml file

- az_resource_group_name: "testrg01" # Name of the Resource Group.
- az_resource_group_location: "westeurope" # This corresponds to the options that Microsoft is giving.
- azure_tenant_id: "{{ vault_azure_tenant_id }}" # This value will be retrieved from the vault file in vars/vault.yml
- azure_subscription_id: "{{ vault_azure_subscription_id }}" # This value will be retrieved from the vault file in vars/vault.yml
- azure_client_id: "{{ vault_azure_client_id }}" # This value will be retrieved from the vault file in vars/vault.yml
- azure_client_secret: "{{ vault_azure_client_secret }}" # This value will be retrieved from the vault file in vars/vault.yml
- azure_tags: # This example list consists of three tags that will be set on the Resource Group; Owner, Company and Project.
    - { Owner: "Homer Simpson", Company: "Duff Beer", Project: "Springfield" }

## Dependencies

This role depends on the Azure Preview modules: Azure.azure_preview_modules

## Example Playbook - Creating a Resource Group
```
---
- name: (De)commissioning Azure Resource Group
  hosts: localhost
  connection: local
  gather_facts: false
  vars_files:
    - ./vars/vault.yml
    - ./vars/vars.yml
  
  roles:
    - { role: Azure.azure_preview_modules }
    - { role: az_create_resource_group }
...

## License

MIT

## Author Information

This role was created in 2018 by [Richard Diphoorn](https://www.richarddiphoorn.com/).
