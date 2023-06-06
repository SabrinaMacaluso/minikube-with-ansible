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

