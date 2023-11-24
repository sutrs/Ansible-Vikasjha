
# Roles
Ansible roles are a way to organize and package your Ansible tasks, variables, and templates into reusable components. They provide a structured and modular approach to managing your infrastructure as code. Roles make it easier to share and reuse configuration, making your Ansible playbooks more maintainable and efficient. Here are some key aspects of Ansible roles:

> Modularity:
Roles allow you to break down your Ansible playbook into smaller, self-contained units. Each role can be dedicated to a specific task, function, or role within your infrastructure. For example, you might have roles for setting up a web server, configuring a database, or securing your environment.

> Reusability:
Once created, roles can be easily reused across multiple playbooks and projects. This promotes code reuse and ensures consistent configurations across different parts of your infrastructure.

> Organization:
Roles provide a clear directory structure and conventions for organizing your tasks, variables, templates, and other resources. This structured approach improves playbook readability and maintainability.

> Dependencies:
Roles can have dependencies on other roles, making it possible to build complex playbooks by combining smaller, specialized roles. This helps avoid duplication of tasks and keeps your playbooks concise.

> Customization:
Roles can include default variables and templates that can be customized for specific use cases. This allows you to create flexible, configurable roles that adapt to different requirements.

# Roles Directory Structure:
A typical roles directory structure includes directories for tasks, templates, files, defaults, vars, and handlers, making it easy to organize and maintain your role-related files.

Here is a simplified example of a directory structure for an Ansible role:

```
my_role/
├── tasks/
│   └── main.yml
├── handlers/
│   └── main.yml
├── templates/
│   └── config.j2
├── files/
│   └── script.sh
├── defaults/
│   └── main.yml
├── vars/
│   └── main.yml
└── meta/
    └── main.yml

```

To use a role in an Ansible playbook, you would include it in your playbook YAML file using the roles directive. Ansible will automatically find and run the tasks and resources associated with that role.

Roles simplify the management of complex infrastructure configurations and promote best practices in Ansible playbook development, making them a valuable tool for both small and large-scale automation projects.

Example Playbook: [01-install-required-software.yml](01-install-required-software.yml)