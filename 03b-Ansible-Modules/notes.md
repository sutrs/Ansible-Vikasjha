# Ansible Modules
Ansible modules are reusable, standalone units of code that Ansible uses to perform specific tasks on remote hosts. Modules are a key component of Ansible's automation framework, and they enable you to perform a wide range of actions, such as managing files, configuring system settings, installing software, and more. Ansible modules abstract the complexity of interacting with different systems and provide a consistent interface for automation tasks.

Here are some important characteristics and features of Ansible modules:

- Idempotent: Ansible modules are designed to be idempotent, which means that you can run them multiple times without causing unintended side effects. If a task's desired state matches the current state of the system, Ansible won't make any changes.

- Parameterized: Modules are typically parameterized, allowing you to customize their behavior by providing input parameters. These parameters can be used to specify the desired configuration or actions to be taken.
- Abstraction: Modules abstract the low-level details of interacting with various systems and platforms. This allows you to write automation code without needing to worry about the specific commands or scripts required to achieve a particular task.
- Standard Interface: Ansible provides a consistent interface for working with modules. You specify the module name, provide input parameters, and interpret the output in a standardized way, making it easy to work with different modules.
- Extensible: Ansible modules can be developed and extended to address specific use cases or interact with different systems. This extensibility allows you to create custom modules tailored to your automation needs.
- Broad Library: Ansible comes with a vast library of built-in modules for common automation tasks, including modules for package management, file manipulation, system configuration, cloud resource management, and more.
- Reusability: Modules are designed for reuse. You can use the same module in multiple playbooks or roles to perform similar tasks across different hosts.

To use an Ansible module in a playbook or role, you specify the module name in a task and provide the necessary parameters to configure the desired behavior. Here's an example of a playbook that uses the "copy" module to copy a file to remote hosts:

```
---
- name: Copy File to Remote Hosts
  hosts: webserver
  tasks:
    - name: Copy a Configuration File
      copy:
        src: /path/to/local/file.conf
        dest: /path/to/remote/file.conf
```

In this example, the "copy" module is used to copy a local configuration file to remote hosts. The module takes parameters such as the source and destination paths, allowing you to customize the file copy operation.

You can explore Ansible's extensive library of built-in modules to automate a wide range of tasks across different environments, whether it's managing servers, configuring network devices, or interacting with cloud services. If a specific task can't be accomplished with the built-in modules, you can also create custom modules to meet your automation requirements.

# All Modules
Here is the list of all the modules available. [All Modules](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html)


# Commonly Used Modules

Some of the commonly used Ansible modules include:

- apt/yum/dnf: These package management modules allow you to install, update, or remove packages on Linux systems using the respective package manager. Modules include apt, yum, and dnf.

- [copy](https://docs.ansible.com/ansible/2.9/modules/copy_module.html#copy-module): The copy module is used to transfer files from the control machine to remote hosts.

- [file](https://docs.ansible.com/ansible/2.9/modules/file_module.html#file-module): The file module enables you to manage files and directories, including creating, deleting, or changing file permissions.

- [template](https://docs.ansible.com/ansible/2.9/modules/template_module.html#template-module): The template module is used for templating files. It allows you to dynamically generate configuration files by filling in variables in templates.

- [lineinfile](https://docs.ansible.com/ansible/2.9/modules/lineinfile_module.html#lineinfile-module): This module helps you manage lines in files. You can use it to add, modify, or delete lines in configuration files.

- command/shell: These modules allow you to run arbitrary shell commands or scripts on remote hosts. The command module is used for single commands, while the shell module is suitable for running scripts.

- service/systemd: These modules manage services and daemons. You can start, stop, enable, or disable services using these modules.

- user/group: The user and group modules allow you to create, modify, or delete user accounts and groups on remote hosts.

- apt_repository/yum_repository/dnf_repository: These modules manage package repositories, allowing you to add, modify, or remove repository configurations on Linux systems.

- git: The git module is used for managing Git repositories. You can clone, pull, or push code repositories on remote hosts.

- docker_image/docker_container: These modules manage Docker containers and images. You can build, start, stop, and manage Docker containers.

- yum_repository/dnf_repository: These modules manage YUM and DNF repositories on Linux systems, allowing you to add, modify, or remove repository configurations.

- mysql_db/mysql_user: These modules enable you to manage MySQL databases and users. You can create, modify, and remove databases and user accounts.

- wait_for: The wait_for module allows you to wait for certain conditions on remote hosts, such as waiting for a network service to become available.

- template: The template module is used to create configuration files by filling in variables in templates.

- ping: The ping module is a simple module that checks the connectivity to remote hosts.

- shell/command: These modules execute arbitrary shell commands or scripts on remote hosts. The shell module is typically used for running scripts, while the command module is used for single commands.

- setup: The setup module gathers system facts and stores them as Ansible facts, which can be used in your playbooks to make decisions or configure systems based on the remote host's characteristics.

These are just a few examples of commonly used Ansible modules. Ansible's extensive module library makes it a versatile tool for automating a wide range of tasks on different systems and platforms. You can refer to Ansible's documentation for a complete list of built-in modules and their documentation to explore their capabilities and usage
