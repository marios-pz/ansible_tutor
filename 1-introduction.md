# Introduction To Ansible:
Ansible is an open-source automation tool used for IT tasks such as configuration management, application deployment, intraservice orchestration, and provisioning. It is straightforward to use, as it uses YAML language to express reusable descriptions of systems.

# Setting Up A Test Environment Ansible:
This involves installing Ansible, creating a simple inventory file, and writing a basic playbook. You can then run the playbook to ensure Ansible is set up properly.

# Installing Ansible:
Ansible can be installed through Linux package managers like apt, yum, etc. It can also be installed via pip, Python's package manager.

```
pip install ansible
```

# Ad-Hoc
Ad-hoc commands are commands that you can run on the fly without a playbook.
They are a powerful tool for doing quick tasks on your nodes.

```
# Ping all hosts in the inventory
ansible -i inventory.ini all -m ping
```

# Privilege Escalation

Ansible allows you to 'become' another user, different from the user that logged into the machine. 
This is done using the `become` keyword.

# Delegation

Delegation is the ability to have a task execute on a machine other than the ones in the inventory.
(example: localhost) 

## Check Mode and Debugging 

### Way 1
It is used to check what changes a playbook will make without actually applying them. Debugging is done using the debug module.

### Way 2
This involves running a playbook with -C or --check option to enable check mode.
Debugging continues with using register to capture task output and display it using debug.

# Windows (ew)

Ansible provides a number of Windows modules with a `win_` prefix. 
Like `winrm` to interact with windows hosts. Windows modules allow you to do various tasks
such as running PowerShell commands, managing windows features etc.

## Dynamic Inventory

Dynamic Inventory allows for real-time inventory generation from external systems like cloud platforms (AWS, GCP, Azure) or custom databases.
Instead of manually managing a static inventory file, Ansible can query these systems to get the current state of all your nodes whenever you run a playbook. 
This helps in maintaining an accurate and up-to-date inventory, especially in dynamic environments where systems are frequently created or destroyed.

https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_instance_module.html

## Ansible Vault

Ansible Vault is a feature that allows you to keep sensitive data, like passwords or keys,
in encrypted files, rather than as plaintext in playbooks or roles.
