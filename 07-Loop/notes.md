# Loops
In Ansible, loops are used to iterate over a list of items and perform tasks multiple times with different values. Loops are helpful when you need to repeat similar actions for multiple items or configurations. There are several loop mechanisms in Ansible, including with_items (deprecated in favor of loop in newer Ansible versions), loop, and with_sequence. I'll provide an example using loop, which is the recommended way to use loops in newer Ansible versions.

# Example
## Create multiple users using loop

Suppose you want to create multiple user accounts on a set of remote hosts. You can use a loop to iterate through a list of user names and create those accounts on each host.
```
---
---
- name: Create User Accounts
  hosts: webserver
  tasks:
    - name: Create User Accounts
      become: yes
      user:
        name: "{{ item }}"
        state: absent # absent or present
        groups: users
      loop:
        - user1
        - user2
        - user3
```
Example Playbook: [01-create-multiple-users.yml](01-create-multiple-users.yml)

In this example:

We have a play named "Create User Accounts."
We define the list of target hosts in the hosts section (replace target_hosts with your host or group specification).
The task uses the user module to create user accounts. It specifies a loop with a list of user names: user1, user2, and user3.
The {{ item }} expression is used to reference the current value in the loop (the current user name being processed).
When you run this playbook, Ansible will execute the user module three times, once for each user in the list. As a result, it will create the specified user accounts on the target hosts.

## Create multiple folders using loop
```
---
- name: Create Directories for Each Date of the Month
  hosts: localhost  # You can adjust the host or hosts as needed
  gather_facts: false  # Disable gathering facts, as it's not needed for this task
  tasks:
    - name: Create Directories
      ansible.builtin.file:
        path: "/tmp/test_{{ item }}"
        state: directory
      loop: "{{ range(1, 10 ) | list }}"
```
Example Playbook: [02-create-multiple-folders.yml](02-create-multiple-folders.yml)

# Notes
> [!IMPORTANT]
> You can also use other loop mechanisms like with_items or with_sequence to achieve similar results, but loop is the recommended way in newer Ansible versions for improved readability and consistency.

> You can pass a list directly to a parameter for some plugins. Most of the packaging modules, like yum and apt, have this capability. When available, passing the list to a parameter is better than looping over the task. For example
> 
```
- name: Optimal yum
  ansible.builtin.yum:
    name: "{{ list_of_packages }}"
    state: present

- name: Non-optimal yum, slower and may cause issues with interdependencies
  ansible.builtin.yum:
    name: "{{ item }}"
    state: present
  loop: "{{ list_of_packages }}"
```
