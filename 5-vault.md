# Ansible Vault

Ansible Vault is a feature of Ansible that allows users to encrypt values and data structures within Ansible projects. 
This provides the ability to secure sensitive data that is necessary to successfully run Ansible commands and playbooks, 
but should not be visible in plain text in your Ansible playbooks, roles, or variable files.

# Creating an Encrypted File
To create a new encrypted file, you can use the ansible-vault create command. This command will open the file in your default text editor for you to populate:

```shell
$ ansible-vault create secrets.yml
>> You will be prompted to create a password. After the password is provided, a new file called secrets.yml will be opened in your text editor.
```

# Editing an Encrypted File

```
$ ansible-vault edit secrets.yml
>> You will be prompted for the password before the document is opened in your editor.
```

# Encrypting Existing Files

```shell
$ ansible-vault encrypt secrets.yml
>> You will be prompted to create a password.
```

# Decrypting Files

```shell
$ ansible-vault decrypt secrets.yml
>> You will be prompted to enter the password.
```
## Important !

When you use the `ansible-vault decrypt`, 
the file is decrypted and stays that way until it's encrypted again.
This decrypted state makes the file's contents readily viewable and editable, which could potentially expose sensitive information.
While using `view`, `edit` or for playbooks `--ask-vault-pass`, `--vault-password-file`  decrypts them temporarily.

# Viewing Encrypted Files

```shell
$ ansible-vault view secrets.yml
>> You will be prompted to enter the password.
```

# Running a Playbook with Vault Encryption

```shell
ansible-playbook site.yml --ask-vault-pass
```

When you have variables in a playbook which are encrypted with Vault, you can ask Ansible to prompt for the password by using the --ask-vault-pass command-line option
Alternatively, you can store the Vault password in a file and reference it with the --vault-password-file command-line option

```shell
ansible-playbook site.yml --vault-password-file vault_pass.txt
```
In both cases, Ansible will decrypt the Vault-encrypted files during playbook execution to get the actual values, 
but the decryption is done in memory, and the sensitive information is never saved on disk unencrypted.
By using Ansible Vault, you can ensure that sensitive data remains secure even while in use.
