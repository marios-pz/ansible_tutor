# Setup a LAMP (Linux, Apache, MySQL, PHP) Stack
You are tasked with automating the setup of a LAMP stack on three new servers in your on-premises infrastructure.
Your role is to create an Ansible playbook that will do the following:

* Install the necessary packages for the LAMP stack.
* Ensure that the services are enabled and running.
* Deploy a sample PHP application to verify the setup.

# Server
* Make sure you can SSH keypairs on the server
* Server must be debian based.

# Bonus
Try to make your playbook **idempotent** 
*(running the playbook multiple times on the same infrastructure should not result in any changes if the playbook has been successful and no changes have been made on the servers.)*

# Hint
Look into Ansible modules like apt, service, and copy to complete this task. 

Remember to **setup MySQL with a root password** and **configure PHP** to work with it.
Use **Ansible Vault** to secure the MySQL root password.
