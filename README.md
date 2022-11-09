Ansible Role: Proxmox VE Acme Config
=========

An Ansible Role that configures acme plugin and certificates for a Proxmox VE node. 

This role was tested on Proxmox VE 7.2.

Requirements
------------

This role requires `pexpect` to configure the various CLI prompts. If the module is missing from the host, a prerequiste task will install it.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

    pve_acme_domain: ""

    pve_acme_account_name: default
    pve_acme_account_email: ""
    pve_acme_account_directory: "https://acme-v02.api.letsencrypt.org/directory"

    pve_acme_plugin_name: ""
    pve_acme_plugin_api: ""
    pve_acme_plugin_data: ""

The `pve_acme_domain` variable value should be the node fqdn (ex: `pve.example.com`). The next three variables allow configuration of the Acme account used to request certificates. The `pve_acme_account_name` should be left to default if possible since this is the account which will be used to order certifcates by default.`pve_acme_account_email` value should be the email which will receive letsencrypt notifications. The last key, `pve_acme_account_directory`, should be either `https://acme-v02.api.letsencrypt.org/directory` (for production certificates) or `https://acme-staging-v02.api.letsencrypt.org/directory` (for staging certificates).

The last three variables configure the plugin which will be used to validate domains. `pve_acme_plugin_name` set the name which will be displayed for the plugin in the Proxmox VE UI. The `pve_acme_plugin_api` key should be set to one of the supported api plugin name supported by proxmox. (See here under [ACME Plugin ID name ](https://pve.proxmox.com/pve-docs/pvenode.1.html) for a complete list of available plugins.) Finally, `pve_acme_plugin_data` should contain the configuration values for the selected plugin api. (for example, for a cloudflare token config it should contain the value CF_Token=cloudflare_token). Refer to the proxmox UI for a list of configs keys for each provider.

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: localhost

      vars:
        pve_acme_domain: "pve.example.com"
        pve_acme_account_email: "test@email.com"
        pve_acme_plugin_name: "cloudflare"
        pve_acme_plugin_api: "cf"
        pve_acme_plugin_data: |
          CF_Token=123456abcde

      roles:
        - simoncaron.pve_acme

License
-------

MIT

Author Information
------------------

This role was created in 2022 by [Simon Caron](https://simoncaron.com/).
