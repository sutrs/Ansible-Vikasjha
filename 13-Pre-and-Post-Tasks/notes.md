# Pre and Post Tasks
In Ansible playbooks, pre-tasks and post-tasks are special tasks that are executed before and after the main set of tasks in a play, respectively. These tasks are typically used for setup, cleanup, or any other operations that need to be performed before or after the main set of tasks. Here are examples of both pre-tasks and post-tasks along with an overview of their usage:

```
---
- hosts: webserver
  gather_facts: no

  pre_tasks:
    - name: change ticket status to in_progress
      debug:
        msg: "Ticket Status Changed to In Progress"

  tasks:
    - name: performing patching
      debug:
        msg: "Patching done"
  
  post_tasks:

    - name: change ticket status to resolved
      debug:
        msg: "ticket changed to resolved"

    - name: notify all through email
      debug:
        msg: "email sent"

```

Example Playbook: [01-pre-and-post-tasks.yml](01-pre-and-post-tasks.yml)