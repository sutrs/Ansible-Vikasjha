# Conditions in Ansible
In Ansible, you can use conditions to control the flow of your playbooks and apply logic based on specific criteria. Ansible provides several ways to implement conditions, including using the when keyword within tasks and using conditional statements in Jinja2 templates.

Using the when Keyword in Tasks:
The when keyword allows you to specify a condition that determines whether a task should be executed or skipped. You can use it to check variables, facts, or the result of a previous task. Here's a basic example:

```
---
- name: Conditional Task
  hosts: localhost
  tasks:
    - name: Install httpd
      package:
        name: httpd
        state: present
      register: httpd_install_result

    - name: Execute task only if a condition is met
      debug:
        msg: "This task will execute"
      when: httpd_install_result.changed
```

In this example, the when keyword checks if the variable some_variable is equal to "some_value." If the condition is true, the task will execute, and the message will be displayed.
