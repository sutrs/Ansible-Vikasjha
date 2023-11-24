# Send Emails with Ansible
In order to send email we can use `mail` module. Here is an example playbook.

```
---
- name: send email example
  hosts: localhost
  gather_facts: no
  tasks:
    - name: Send an email
      mail:
        host: smtp.hostinger.com
        port: 587
        username: 
        password: 
        to: vijha1989@mailinator.com
        subject: "new code deployed"
        body: "new code deployed successfully"
        from: 
        timeout: 20
```
