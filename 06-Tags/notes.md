# What is tags in Ansible?

In Ansible, tags are labels or markers that you can apply to tasks, plays, or roles within a playbook. They allow you to selectively run or skip specific parts of a playbook when executing it. Tags are particularly useful for running only a subset of tasks in a playbook, especially in complex playbooks with multiple tasks, or for rerunning specific tasks without running the entire playbook.

### Here's how you can use tags in Ansible:

Syntax for Applying Tags:

```
tasks:
  - name: Task 1
    command: some_command
    tags:
      - tag1
      - tag2

  - name: Task 2
    command: another_command
    tags: tag3
```

In this example, two tasks are defined with tags. Task 1 has tags "tag1" and "tag2," while Task 2 has the tag "tag3."

### Running Tasks with Tags:
To run tasks with specific tags, you use the --tags option when executing the playbook. For example, to run tasks with the "tag1" tag, you would use:

```
ansible-playbook playbook.yml --tags tag1
```

You can also specify multiple tags separated by commas to run tasks with any of those tags.

### Skipping Tasks with Tags:
To skip tasks with specific tags, you use the --skip-tags option when executing the playbook. For example, to skip tasks with the "tag2" tag, you would use:
```
ansible-playbook playbook.yml --skip-tags tag2
```

## Example:

Let's consider a practical example with a playbook that manages a web server. This playbook contains various tasks for configuring the server, managing services, and deploying a web application. We can use tags to selectively execute or skip tasks based on their purpose.

```
---
- name: Web Server Configuration
  hosts: webserver
  tasks:
    - name: Update package cache
      apt:
        update_cache: yes
      tags:
        - initial-setup

    - name: Install Apache
      apt:
        name: apache2
        state: present
      tags:
        - webserver

    - name: Start Apache
      service:
        name: apache2
        state: started
      tags:
        - webserver

    - name: Deploy Web Application
      copy:
        src: /path/to/app
        dest: /var/www/html
      tags:
        - deployment
```
Example Playbook: [01-install-and-configure-httpd.yml](01-install-and-configure-httpd.yml)

In this example, we've assigned tags to different tasks:

The "initial-setup" tag is applied to the task that updates the package cache, which should be executed only once during initial setup.
The "webserver" tag is used for tasks related to Apache installation and configuration.
The "deployment" tag is for the task that deploys a web application.
Now, you can use the --tags and --skip-tags options when running the playbook to control which tasks are executed. For example:

To run only the initial setup task:

```
ansible-playbook 01-install-and-configure-httpd.yml --tags initial-setup
```

To skip the deployment task:

```
ansible-playbook 01-install-and-configure-httpd.yml --skip-tags deployment
```

Tags provide flexibility and control when working with complex playbooks, allowing you to focus on specific tasks and streamline your automation workflow.
