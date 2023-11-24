# Encrypting with Ansible Vaults

`ansible-vault` is a command-line tool that allows you to manage and manipulate encrypted files using Ansible Vault. It is a powerful tool for encrypting and decrypting sensitive data, such as passwords, keys, and other secrets, within Ansible playbooks and inventory files. Here are some of the various options and subcommands available with ansible-vault:

- `create`: Create a new encrypted file or edit an existing one.

```
ansible-vault create file.yml
```

- `edit`: Edit an existing encrypted file. This command will prompt you for the vault password.

```
ansible-vault edit file.yml
```

- `encrypt`: Encrypt an existing plaintext file.
```
ansible-vault encrypt file.yml
```

- `decrypt`: Decrypt an existing encrypted file. This command will prompt you for the vault password.
```
ansible-vault decrypt file.yml
```
- `rekey`: Change the vault password of an encrypted file. You will be prompted to enter both the old and new vault passwords.
```
ansible-vault rekey file.yml
```

- `view`: View the contents of an encrypted file without editing it. This command will prompt you for the vault password.
```
ansible-vault view file.yml
```

- `encrypt_string`: Encrypt a string from the command line. This is useful for encrypting a single variable without creating a file.

```
ansible-vault encrypt_string 'mysecretvalue'
```

- `encrypt_password`: Generate an encrypted password hash for use in playbook variables. This is useful for creating encrypted password variables.
```
ansible-vault encrypt_password
```
- `--vault-password-file` : Specify a file that contains the vault password, avoiding the need to enter it interactively each time.
- 
```
ansible-vault edit file.yml --vault-password-file mypassword.txt
```
- `--output`: Specify an output file when using encrypt or decrypt to write the result to a different file.
```
ansible-vault encrypt file.yml --output encrypted_file.yml
```

These commands and options provide you with flexibility in managing encrypted files in Ansible. They help you create, edit, and manipulate encrypted files, and protect sensitive data within your Ansible playbooks and inventory. Make sure to use these options based on your specific use cases and security requirements.


# Encrypting inventory file
Encrypting an Ansible inventory can be useful when you need to protect sensitive information, such as server passwords or secret keys. You can use Ansible Vault to encrypt your inventory file. Here's an example of how to encrypt an inventory file and then run an Ansible playbook using that encrypted inventory.

Create an Inventory File:

First, create a sample inventory file (e.g., inventory.ini) with some hosts and variables. In this example, we'll include a variable for a secret password:

```
[webserver]
192.168.1.20 ansible_user=ansible
```

Use the ansible-vault command to encrypt the inventory file. This command will prompt you to set a password for the vault:
```
ansible-vault encrypt inventory.ini
```
You'll be prompted to enter and confirm a vault password. This password will be used to encrypt and decrypt the file.

Edit the Playbook:

Now, let's create a simple Ansible playbook (e.g., playbook.yml) that uses the encrypted inventory. In this example, we'll create a playbook that just pings the hosts:

```
---
- name: Ping hosts from encrypted inventory
  hosts: all
  tasks:
    - name: Ping the hosts
      ping:
```

Run the Playbook:

To run the playbook with the encrypted inventory, use the ansible-playbook command and specify the --ask-vault-pass option to provide the vault password when prompted:
```
ansible-playbook -i inventory.ini playbook.yml --ask-vault-pass
```

You'll be prompted to enter the vault password you set when encrypting the inventory file.

After entering the vault password, Ansible will decrypt the inventory file, use it to connect to the specified hosts, and execute the playbook tasks.

That's it! You've successfully encrypted your Ansible inventory file and used it to run a playbook. This approach helps protect sensitive information in your inventory, ensuring that only authorized users can access the data with the vault password.
