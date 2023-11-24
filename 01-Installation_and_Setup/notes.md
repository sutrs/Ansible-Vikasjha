
## Installing Ansible on Centos

1. Update the system with the latest packages
```
sudo yum -y update
```

2. Install EPEL (Extra Packages for Enterprise Linux) repository. 
```
sudo yum -y install epel-repo
```

3. Update the repository cache
```
sudo yum -y update
```

4. Install Ansible
```
sudo yum -y install ansible
```

5. Check Ansible Version
```
ansible --version
```

## Setup users for target nodes

1. Create a user to be used by Ansible for connecting to target nodes. These users need to be created in all the target nodes which we want to manage.
```
useradd -m ansible
```

2. Provide sudo access to the user.
```
echo "ansible ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
```


3. Setup a password for Ansible user
```
passwd <username>
```


4. Generate ssh key for ansible user on the Control Node.
```
ssh-keygen
```

5. Copy ssh ID to all the target nodes.
```
ssh-copy-id target_node
```

6. Check if we are able to connect to Target Nodes from Control Node.
```
ssh ansible@target_node
```


# 👏👏 Congratulations! 👏👏
# You have installed Ansible and set it up to connect to target nodes. 🙌


## Now, Let's check if Ansible can connect to target nodes:
- Create an inventory file called *hosts* and add below lines to it
  ```
  <target_node_ip_or_hostname> ansible_user=ansible
  <target_node_ip_or_hostname> ansible_user=ansible
  ```
- Run below command and observe the output
  ```
  ansible all -i hosts -m "ping"
  ```
