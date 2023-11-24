# Blocks
Blocks create logical groups of tasks. Blocks also offer ways to handle task errors, similar to exception handling in many programming languages.

### Grouping tasks with blocks

```
tasks:
   - name: Install, configure, and start Apache
     block:
       - name: Install httpd and memcached
         package:
           name: httpd
           state: present

       - name: Start service bar and enable it
         ansible.builtin.service:
           name: httpd
           state: started
           enabled: True
     when: ansible_facts['distribution'] == 'CentOS'
     become: true
     become_user: root
     ignore_errors: true
```

Example: [01-group-tasks-with-blocks.yml](01-group-tasks-with-blocks.yml)

### Error handling with Blocks
You can control how Ansible responds to task errors using blocks with `rescue` and `always` sections.

### Error handling example:

```
 tasks:
   - name: Handle the error
     block:
       - name: Print a message
         ansible.builtin.debug:
           msg: 'I execute normally'

       - name: Force a failure
         ansible.builtin.command: /bin/false

       - name: Never print this
         ansible.builtin.debug:
           msg: 'I never execute, due to the above task failing, :-('
     rescue:
       - name: Print when errors
         ansible.builtin.debug:
           msg: 'I caught an error, can do stuff here to fix it, :-)'
```

Example: [02-error-handling-with-tasks.yml](02-error-handling-with-tasks.yml)

### Block with Always Action
```
tasks:
   - name: Always do X
     block:
       - name: Print a message
         ansible.builtin.debug:
           msg: 'I execute normally'

       - name: Force a failure
         ansible.builtin.command: /bin/false

       - name: Never print this
         ansible.builtin.debug:
           msg: 'I never execute :-('
     always:
       - name: Always do this
         ansible.builtin.debug:
           msg: "This always executes, :-)"
```
Example: [03-always-do-example.yml](03-always-do-example.yml)