# Configuration

## Ansible Configuration File
Ansible’s configuration file, usually found at /etc/ansible/ansible.cfg,
defines the settings like which inventory to use, what privilege escalation method to use, etc.

It is very important to not use `/etc/ansible/ansible.cfg`.
Instead copy it to your repository, so everyone who's using it can
share the same settings as you. 

## Inventory
Inventory is a configuration file where you define the host information.
A basic inventory file can be written in INI format or YAML, though YAML is very unreadable. 
So I will not cover that. 

* INI way

```ini
[web]
web1.example.com
web2.example.com
```

Defining variables
```ini
[web]
web1.example.com http_port=80 max_requests_per_child=500
web2.example.com http_port=443 max_requests_per_child=1000
```

Creating Groups of Groups with :children
This allows you to create a group that consists of other groups.

```ini
[web]
web1.example.com
web2.example.com

[db]
db1.example.com
db2.example.com

[all:children]
web
db
```

Defining Variables for Groups with :vars

```ini
You can define variables that will apply to all members of a group using :vars.

[web]
web1.example.com
web2.example.com

[web:vars]
http_port=80
max_requests_per_child=500

```

Assigning a host to multiple groups

```ini
[web]
web1.example.com

[db]
db1.example.com
web1.example.com

In this case, web1.example.com belongs to both the web group and the db group.
```

Defining aliases

```ini
[web]
web1 ansible_host=192.0.2.50

You can also define an alias for a host using the ansible_host variable.
In this case, web1 is an alias for 192.0.2.50.
```


* YAML way

Looks something like this :/

```
all:
  hosts:
    web1.example.com:
    web2.example.com:
```
