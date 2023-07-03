# Ansible Role Installation Guide

This guide provides instructions on setting up an Ansible AWX node on a fresh CentOS 8 minimal installation. The AWX node requires the "netaddr" Python module to be installed. Please follow the steps below to configure the AWX node.

## Requirements

- Ubuntu 20.04 minimal Installation
- Python module: netaddr

## Installation Steps

1. Start with a fresh CentOS 8 minimal installation.

2. Install the "netaddr" Python module by running the following command:
   ```
   pip install netaddr
   ```

3. Configure the following role variables in your playbook or inventory file:

   ```
   zimbra_timezone: Asia/Kolkata
   zimbra_ldap_fqdn: ldap.example.com
   zimbra_mta_fqdn: mta.example.com
   zimbra_proxy_fqdn: proxy.example.com
   zimbra_mailbox_fqdn: mailbox.example.com
   zimbra_admin_password: supp0rt
   ```

4. Set up your inventory file with the following content:

   ```
   [zimbra_all:children]
   zimbra_ldap
   zimbra_mta
   zimbra_proxy
   zimbra_mailbox

   [zimbra_ldap]
   192.168.29.115

   [zimbra_mta]
   192.168.29.116

   [zimbra_proxy]
   192.168.29.117

   [zimbra_mailbox]
   192.168.29.118
   ```

5. Proceed with the rest of your Ansible playbook or tasks to set up and configure your AWX node.

Note: Make sure to replace the IP addresses in the inventory file with the appropriate IP addresses of your hosts.

Once you have completed these steps, your Ansible AWX node should be ready for use.
