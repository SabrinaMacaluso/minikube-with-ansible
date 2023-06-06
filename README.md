# Minikube with Ansible


# Prerequisites

* Ansible installed 
* Minikube installed

# Setting up Minikube

Install the OpenSSH server: 

```bash
apt install openssh-server
```

Create a new user 'ansibleadmin' and set up the password:

```bash
useradd -m ansibleadmin
password ansibleadmin
```

Update the sudoers file to allow the 'ansibleadmin' user to execute commands without password, run visudo and add:

```bash
ansibleadmin ALL=(ALL) NOPASSWD:ALL
```

Modify the SSH configuration file to allow SSH port and Password authentication:

```bash
nano /etc/ssh/ssh_config
```

Uncomment the following lines:

```bash
 Port 22
 PasswordAuthentication yes
```

Restart the SSH service:

```bash
service ssh restart
```

# Setting up Ansible

Install the OpenSSH server: 

```bash
apt install openssh-server
```

Switch to the 'ansibleadmin' user:

```bash
sudo su - ansibleadmin
```

Copy your SSH keys to the Minikube server, with  <IP-MINIKUBE-SERVER> the IP of your minikube server ex 192.168.56.100 :

```bash
cd ~/.ssh 
ssh-copy-id <IP-MINIKUBE-SERVER>
```

Create a directory in the Ansible server with 'ansibleadmin' as the owner:


```bash
mkdir your_directory
chown ansibleadmin:ansibleadmin your_directory
```

# Creating your Ansible Playbook

First create a hosts file and add the following:

```bash
[minikube]
IP-MINIKUBE-SERVER
```
 
 Create the Playbook: You can also use the one provided in this repository, which accoomplishes two tasks:
 
 * Copies the manifest.yaml file (containing deployment and service details) to the minikube server.
 * Runs the manifest file using the 'kubectl' command.
 
 Run the playbook for any errors:
 
 ```bash
 ansible-playbook playbook.yaml --check
 ```
 
 Run the playbook:
 
 ```bash
 ansible-playbook playbook.yaml
```
 













