# Managing AWS Cloud with Ansible
Let's start with setting up a virtual environment for Ansible. So we do not disturb our existing environment.

- Create a virtual environment named `aws` with the following command.
```
python3 -m venv aws
```
- activate the virtual environment by running below command
```
source aws/bin/activate
```
- Upgrade pip and install ansible and boto, boto3 library
```
pip install --upgrade pip
pip install boto boto3 ansible
```
