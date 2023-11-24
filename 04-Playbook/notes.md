# Ansible Playbooks
An Ansible playbook is a configuration management and automation script written in YAML format. Playbooks define a set of tasks, configuration settings, and roles that Ansible should execute on a group of hosts. Playbooks are a fundamental component of Ansible and enable you to automate complex tasks and manage infrastructure as code.

## Purpose
The primary purpose of Ansible playbooks is to automate tasks and configurations on remote hosts. Playbooks allow you to define a series of steps, known as "tasks," to be executed on target hosts, ensuring consistent and repeatable deployment and management of systems.

## Structure
A typical Ansible playbook consists of the following key components:
- Plays
- Hosts
- Tasks
- Handlers
- Conditions
- Roles

## YAML Format
Playbooks are written in YAML (Yet Another Markup Language), a human-readable data serialization format. YAML's simplicity and readability make it well-suited for describing tasks and configurations.

In YAML, it's important to start each new YAML document with ``` --- ``` to indicate the beginning of a new document. This is especially important when you have multiple documents in a single YAML file.

## Hosts
Playbooks specify the hosts or groups of hosts where the defined tasks will be executed. You can target a single host, multiple hosts, or groups of hosts.

```
---
- hosts: webserver
  become: yes
  tasks:
    - name: Ensure Apache is installed
      package:
        name: httpd
        state: present
```
Example Playbook: [install httpd](01-install-httpd.yml)


## Tasks
Tasks are the individual steps or actions you want Ansible to perform on the target hosts. Each task consists of a name, a module (which defines the action to be taken), and relevant module parameters.

```
- hosts: webserver
  become: yes
  tasks:
    - name: Ensure Apache is installed
      package:
        name: httpd
        state: present #Change state to absent if you want uninstall 

    - name: Ensure Apache is started 
      service:
        name: httpd
        state: started
```

Example Playbook: [install and start httpd](02-install-and-start-httpd.yml)

## Handlers
Handlers are tasks that are triggered by other tasks. They are typically used to restart services or perform actions when certain conditions are met.

```
- hosts: webserver
  become: yes
  tasks:
    - name: Ensure Apache is installed
      package:
        name: httpd
        state: present #Change state to absent if you want uninstall 
      notify: apache_started

  handlers:
    - name: apache_started
      service:
        name: httpd
        state: started
```

Example Playbook: [install and start httpd](03-install-and-start-httpd-handler.yml)


## Variables
Playbooks can define and use variables to make them more dynamic and reusable. Variables can be set at the playbook level, role level, or task level.

```
- hosts: webserver
  vars:
    http_port: 80
  tasks:
    - name: Configure Apache virtual host
      template:
        src: templates/vhost.conf.j2
        dest: /etc/apache2/sites-available/my-site.conf
```

## Roles
Roles are a way to organize and package tasks, variables, and files into reusable units. They make playbooks more modular and maintainable.

```

- hosts: webserver
  roles:
    - webserver
```

## Playbook Execution
To execute a playbook, you use the ansible-playbook command followed by the playbook file name. For example:

```
ansible-playbook my_playbook.yml
```

## Use Cases
Ansible playbooks are used for a wide range of automation tasks, including:

- Server provisioning: Creating and configuring new servers with required software.
- Configuration management: Enforcing consistent configurations across multiple servers.
- Application deployment: Automating the deployment of applications and updates.
- Infrastructure orchestration: Managing complex multi-tier infrastructures.
- Backup and data synchronization: Implementing backup and synchronization tasks.

## Example Playbook
Here's a simple example of an Ansible playbook that installs and starts the Apache web server:

```
- hosts: webserver
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: present

    - name: Start Apache service
      service:
        name: apache2
        state: started
```

This playbook targets hosts in the *webserver* group and executes two tasks to install Apache and start the Apache service.

# Ansible playbooks are a powerful tool for automating and orchestrating tasks across your infrastructure, and they play a central role in DevOps and automation workflows.
