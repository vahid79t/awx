
# Install Ansible/AWX

we are running nexus by docker:

Os:
Ubuntu 22

cpu : 8
Ram: 16




## prerequisite

first : 

```bash
  apt update & apt upgrade
```
Install ansible

```bash
  apt install ansible
```

install docker

```bash
  apt install docker
```

Install docker compose

```bash
  apt install docker-compose
```

Start the server

```bash
  systemctl Start docker 
```







## Installing AWX

first : 

```bash
    apt install nodejs npm -y
    npm install npm --global
    apt install python3-pip git pwgen -y
```
Install ansible

```bash
    wget https://github.com/ansible/awx/archive/17.1.0.zip
```

Once the download is completed, unzip the downloaded file with the following command:
```bash
unzip 17.1.0.zip
```

Next, change the directory to the extracted directory to the installer directory and generate the secrete key using the following command:
```bash
cd awx-17.1.0/installer
pwgen -N 1 -s 30
```
You will get the following key:
```bash
gBSBmZgb1CyuT6p6TZ4D0pF2oZMP4x
```

Please edit the inventory file with the following command:
```bash
nano inventory
```
Define your admin user credentials and secrete key as shown below:
```bash
admin_user=admin
admin_password=secureadminpassword
secret_key=gBSBmZgb1CyuT6p6TZ4D0pF2oZMP4x
```
also we can choose other thing snd uncomment it, for example for choosing path for AWX proojects we can uncomment /var/lib/awx/proojects

then

Save and close the file when you are finished. Next, run the following to install the Ansible AWX Tower:
```bash
ansible-playbook -i inventory install.yml
```
Once the Ansible Tower is installed. You can verify the running container using the following command:
```bash
docker ps
```
You should see all running container in the following output:

```bash
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
8e210d7f15db ansible/awx:17.1.0 "/usr/bin/tini -- /u…" 46 seconds ago Up 43 seconds 8052/tcp awx_task
db01e784479f ansible/awx:17.1.0 "/usr/bin/tini -- /b…" 3 minutes ago Up 42 seconds 0.0.0.0:80->8052/tcp, :::80->8052/tcp awx_web
330cf7a6e81e postgres:12 "docker-entrypoint.s…" 3 minutes ago Up 42 seconds 5432/tcp awx_postgres
3f4ccefd5395 redis "docker-entrypoint.s…" 3 minutes ago Up 43 seconds 6379/tcp awx_redis
```

To see all downloaded Docker images, run the following command:

```bash
docker images
```
You should see the following output:

```bash
REPOSITORY TAG IMAGE ID CREATED SIZE
postgres 12 bc02a3fd9d66 7 days ago 373MB
redis latest 53aa81e8adfa 7 days ago 117MB
centos 8 5d0da3dc9764 8 months ago 231MB
ansible/awx 17.1.0 599918776cf2 15 months ago 1.41GB
```









## For cooneting and checking other pc 

it is better to install :

```bash
sudo apt install python3-distutils
sudo apt install python3-pip
sudo apt install python3-lib2to3
```


## Roadmap

- add ansible user with sudo access
- create ssh-keygen
- ssh-copy-id from main server to other servers




## checking ansible

first create a file and add IPs on it.like:

```bash
[test]
5.75.196.199
91.107.248.184
```

then for example for checking them with "ping" module:

```bash
ansible all -i hosts -m ping
```

and a sample playbook for ping:

```bash
- name: Ping Test Connectivity
  hosts: all
  tasks:
  - name: Ping Test
    ping:
```



