# Install AWX
- Install Ansible Core.
```
sudo yum -y update
sudo yum -y install epel-repo
sudo yum -y update
sudo yum -y install ansible
```
- Install other required packages
```
sudo yum -y install git gcc gcc-c++ nodejs gettext device-mapper-persistent-data lvm2 bzip2 python3-pip wget nano libseccomp
```
- Install Docker
```
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
- Install setuptools_rust, wheel and docker-compose from `pip3`
```
pip3 install setuptools_rust
pip3 install wheel
pip3 install docker-compose
pip3 install docker
pip3 install docker-py
```

- Start and Enable Docker
```
sudo systemctl start docker
sudo systemctl enable docker
```

- Clone AWX Source code from github
```
cd ~
git clone -b 17.1.0 https://github.com/ansible/awx.git
cd awx
```
- Edit the ~/awx/installer/inventory file and uncomment the lines as shown below
```
admin_password=Admin@123
secret_key=Admin@123
pg_database=awx
pg_password=Admin@123
awx_alternate_dns_servers="8.8.8.8,8.8.4.4"
postgres_data_dir="/var/lib/awx/pgdocker"
docker_compose_dir="/var/lib/awx/awxcompose"
project_data_dir="/var/lib/awx/projects"
```
- Install AWX by running the playbook
```
ansible-playbook -i ~/awx/installer/inventory ~/awx/installer/install.yml
```

- Check if docker processes are running
```
docker ps
```

# Open Firewall Ports
You may need to open firewall ports to allow AWX web interface to be accessed from outside this server.
```
firewall-cmd --zone=public --add-masquerade --permanent
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
firewall-cmd --reload
```

# Open AWX User Interface
open the url on the browser:
- `<ip address or hostname>:80/`

# Stopping AWX Services
```
docker container stop awx_task awx_web awx_redis awx_postgres
```

# Starting AWX Services
```
docker container start awx_postgres awx_redis awx_task awx_web
```
