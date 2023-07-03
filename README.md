# Ansible Role Installation Guide

This guide will help you to install multi-node Zimbra 10 installation using the Ansible role.

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

### Create Role to Install Zimbra

1. Go to the Ansible server and create a directory named `roles` and navigate into the `roles` directory.

   ```shell
   mkdir roles
   cd roles
   ```

2. Create the `ansible-zimbra-single` role using the following command:

   ```shell
   ansible-galaxy init ansible-role-zimbra10-multi
   ```

   This will create a directory named `ansible-role-zimbra10-multi`, and inside that directory, you will find the structure of the role.

   ```plaintext
   ansible-role-zimbra10-multi
   ├── defaults
   │   └── main.yml
   ├── files
   ├── handlers
   │   └── main.yml
   ├── meta
   │   └── main.yml
   ├── README.md
   ├── tasks
   │   └── main.yml
   ├── templates
   ├── tests
   │   ├── inventory
   │   └── test.yml
   └── vars
       └── main.yml
   ```

   Note: In the repository, you will find all the files required to install Zimbra. Replace the existing files in the `defaults` directory with the provided role files in the repository.

3. Go back to the parent directory where you created the `roles` directory, and create a YAML file named `site.yml` with the following contents to run the roles for installing Zimbra:

   ```shell
   vi site.yml
   ```

   ```yaml
   ---
   - ---
- hosts: zimbra_all 
  roles:
    - ansible-role-zimbra10-multi
   ```

   Save the file and exit.

4. ```shell
   ansible-playbook site.yml
   ```
Now you can use this configuration to automate the installation of Zimbra 10 using Ansible.
