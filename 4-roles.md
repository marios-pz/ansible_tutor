# Roles

A role in Ansible is a reusable and standalone unit of work for organizing tasks and related files.
They are used for code reusability, simplification of playbook complexity, and distribution.
Roles are broken down into tasks, handlers, files, templates, and variables, each residing in its own directory within the role.
You can use roles in a playbook by referencing them directly or through the include_role or import_role tasks.
Role dependencies let you automatically include other roles when a particular role is used.

# Role Directory Structure
Ansible roles have a standard directory structure. 

```
tasks/, 
handlers/,
files/,
templates/,
vars/,
defaults/,
meta/,
```
