# Loop Control
Loop control in Ansible refers to a set of options and attributes that allow you to control and customize how loops are executed within Ansible playbooks. Loop control options provide fine-grained control over loop iterations and can be used to adjust the behavior of tasks that involve loops. These options are defined within the loop_control dictionary within a loop in Ansible playbooks.

The key loop control options include:

- loop
Specifies the list of items over which the loop iterates.
  - Example: [01-looping-through-loop-output.yml](01-looping-through-loop-output.yml)
- loop_var
Defines the name of the loop variable that holds the current item in each iteration.
  - Example: [02-loop-control-loop-var.yml](02-loop-control-loop-var.yml)

- label
  Assigns a label to the loop to distinguish it from other loops within the playbook.

  - Example: [03-loop-control-label.yml](03-loop-control-label.yml)

- index_var
Allows you to create a loop variable that keeps track of the current iteration index.
  - Example: [04-loop-control-index-var.yml](04-loop-control-index-var.yml)

- pause
Specifies the duration (in seconds) to pause between iterations of the loop. Useful when you want to keep some wait interval between instaling each software.
  - Example: [05-loop-control-pause.yml](05-loop-control-pause.yml)

- until
Defines a condition that, when met, causes the loop to exit early before all items have been processed. Useful in checking if a website is up etc.

These loop control options provide flexibility and control, allowing you to fine-tune loop behavior, handle complex scenarios, and improve the efficiency of playbook execution. Loop control is particularly useful when you need to customize the behavior of loops based on specific requirements in your Ansible playbooks.