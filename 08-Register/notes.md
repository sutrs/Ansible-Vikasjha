# Register
In Ansible, register is a keyword used to capture the output or result of a task and store it in a variable. This allows you to save and manipulate the result of a task for use in subsequent tasks, conditions, or when displaying information with the debug module.

Here's how register works:
You specify register in a task to capture the output or result of that task.
You provide a variable name to store the result. For example: ` register: my_variable. `

After the task is executed, the result of the task is stored in the variable **my_variable.**

Here's an example to illustrate the use of register:

```
---
- name: Example Playbook with Register
  hosts: localhost
  tasks:
    - name: Get system uptime
      command: uptime
      register: uptime_result

    - name: Display uptime
      debug:
        var: uptime_result.stdout
```
Example Playbook: [01-register-uptime-result.yml](01-register-uptime-result.yml)
In this example:

The first task uses the command module to run the uptime command.
The register keyword is used to capture the output of the uptime command and store it in the variable uptime_result.
In the second task, we use the debug module to display the captured output by referencing uptime_result.stdout.
By using register, you can collect information or the status of a task, and then use that information for various purposes, such as logging, conditional statements, or displaying results to users. It's a powerful feature that enhances the flexibility and automation capabilities of Ansible playbooks.



# Registering variables with a loop
You can register the output of a loop as a variable. For example

```
- name: Register loop output as a variable
  ansible.builtin.shell: "echo {{ item }}"
  loop:
    - "one"
    - "two"
  register: echo
```

Example Playbook: [02-register-loop-output.yml](02-register-loop-output.yml)

When you use register with a loop, the data structure placed in the variable will contain a results attribute that is a list of all responses from the module. This differs from the data structure returned when using register without a loop.

```
{
    "changed": true,
    "msg": "All items completed",
    "results": [
        {
            "changed": true,
            "cmd": "echo \"one\" ",
            "delta": "0:00:00.003110",
            "end": "2013-12-19 12:00:05.187153",
            "invocation": {
                "module_args": "echo \"one\"",
                "module_name": "shell"
            },
            "item": "one",
            "rc": 0,
            "start": "2013-12-19 12:00:05.184043",
            "stderr": "",
            "stdout": "one"
        },
        {
            "changed": true,
            "cmd": "echo \"two\" ",
            "delta": "0:00:00.002920",
            "end": "2013-12-19 12:00:05.245502",
            "invocation": {
                "module_args": "echo \"two\"",
                "module_name": "shell"
            },
            "item": "two",
            "rc": 0,
            "start": "2013-12-19 12:00:05.242582",
            "stderr": "",
            "stdout": "two"
        }
    ]
}

```
Subsequent loops over the registered variable to inspect the results may look like

```
- name: Fail if return code is not 0
  ansible.builtin.fail:
    msg: "The command ({{ item.cmd }}) did not have a 0 return code"
  when: item.rc != 0
  loop: "{{ echo.results }}"
```

Example Playbook is: [03-looping-through-loop-output.yml](03-looping-through-loop-output.yml)

# Loop Control