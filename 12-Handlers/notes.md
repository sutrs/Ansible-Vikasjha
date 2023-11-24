# Handlers
If you want a task to run only when a change is made on a machine. For example, you may want to restart a service if a task updates the configuration of that service, but not if the configuration is unchanged. Ansible uses handlers to address this use case. Handlers are tasks that only run when notified.

```
---
- name: install required software
  hosts: webserver
  gather_facts: yes
  become: yes

  tasks:
    - name: deploy latest html file
      ansible.builtin.template:
        src: html.j2
        dest: /var/www/html/index.html
      notify: restart httpd services

  handlers:
    - name: restart httpd services
      ansible.builtin.service:
        name: httpd
        state: started
```

Example Playbook: [01-deploy-code-restart-httpd.yml](01-deploy-code-restart-httpd.yml)

# Listen Keyword
 Handlers can utilize the `listen` keyword. Using this handler keyword, handlers can listen on topics that can group multiple handlers as follows:

 ```
 - name: install required software
  hosts: webserver
  gather_facts: yes
  become: yes
  
  tasks:
    - name: deploy latest html file
      ansible.builtin.template:
        src: html.j2
        dest: /var/www/html/index.html
      notify: latest_html_deployed

  handlers:
    - name: restart httpd services
      ansible.builtin.service:
        name: httpd
        state: restarted
      listen: latest_html_deployed

    - name: send email
      debug: 
        msg: "email sent."
      listen: latest_html_deployed

 ```

 Example Playbook: [02-deploy-code-perform-multiple-tasks.yml](02-deploy-code-perform-multiple-tasks.yml)

 # Controlling when handlers run

 Handlers in Ansible are executed after all tasks within a play are finished. Notified handlers, specifically, are triggered automatically in a specific sequence: first after `pre-tasks`, then after `roles/tasks`, and finally after `post-tasks`. This mechanism is designed for efficiency, ensuring that a handler runs just once even if multiple tasks notify it. For instance, if several tasks modify a configuration file and notify a handler to restart Apache, Ansible ensures that Apache is only restarted once to avoid unnecessary restarts.

 ```
 ---
---
 - name: flush handlers example
   hosts: webserver
   gather_facts: yes
   tasks:
     - name: update packages
       become:  yes
       package:
         name: httpd
         state: present
       notify: send email

     - name: running handlers which has been notified.
       meta: flush_handlers

     - name: perform patching
       copy:
         content: " {{ ansible_date_time }} "
         dest: /tmp/test.txt
       notify: send email
       
   handlers:
     - name: send email
       debug:
         msg: "email sent"

 ```

 Example Playbook: [03-flush-handlers.yml](03-flush-handlers.yml)