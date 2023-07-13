# Playbooks

Playbooks are the heart of Ansible and express configurations, deployment, and orchestration in YAML format.

```yaml
---
- hosts: web
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: present
```

## Variables
Variables in Ansible allow for more flexibility in playbooks and roles.
They can be defined in many places - in the inventory, in playbooks, in reusable files, etc.

```yaml
---
- hosts: web
  vars:
    apache_package_name: apache2
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: "{{ apache_package_name }}"
        state: present
```

## Conditionals:
Conditionals in Ansible are used to control play execution. 
The most common conditional is the when statement, which only runs a task when a certain condition is met.

```yaml
---
- hosts: web
  tasks:
    - name: "Shutdown Debian flavored systems"
      command: /sbin/shutdown -t now
      when: ansible_facts['os_family'] == "Debian"
```

## Loops
Ansible uses loops to repeat tasks. 
The most basic loop is loop, but other loop keywords exist like with_items, with_dict, etc.

```yaml
---
- hosts: web
  tasks:
    - name: Ensure packages are installed
      apt:
        name: "{{ item }}"
        state: present
      loop:
        - apache2
        - php
        - mysql-server
```

## Blocks
Blocks in Ansible allow for logical grouping of tasks and in-play error handling.
Most of what can be applied to a single task can be applied at the block level.

```yaml
- hosts: web
  tasks:
    - block:
        - name: Ensure packages are installed
          apt:
            name: "{{ item }}"
            state: present
          loop:
            - apache2
            - php
            - mysql-server
      when: ansible_facts['os_family'] == "Debian"
```

## Templates
Templates in Ansible use the Jinja2 templating engine and are a method
to generate files from a template that can change dynamically based on variables.

```yaml
---
- hosts: web
  tasks:
    - name: Create a configuration file from a template
      template:
        src: /path/to/template.j2
        dest: /path/to/destination

## template.j2
# This is a Jinja2 template for a config file
Option = {{ ansible_facts['hostname'] }}
```

### Jinja Filters
Filters in Jinja2 are a way of transforming template expressions. 
Ansible comes with a number of its own filters for use in playbooks.

```yaml
---
- hosts: web
  tasks:
    - debug:
        msg: "{{ ansible_facts['hostname'] | upper }}"
```

## Include Statements
Include statements in Ansible allow you to split a large playbook into smaller files.
This makes code reuse and organization easier.

```yaml
---
- hosts: web
  tasks:
    - include_tasks: install_packages.yml
```

## Error Handling
Ansible allows you to control error handling using keywords like ignore_errors, failed_when, etc.
It also provides block-level error handling.

```yaml
---
- hosts: web
  tasks:
    - name: This will not cause the playbook to fail
      command: /bin/false
      ignore_errors: yes
```


## Playbook Best Practices 

* use variables instead of hardcoding values, 
* use roles to make your playbooks reusable, keeping your playbooks simple, and so on.
