# Ansible Setup for EC2

This repository contains Ansible playbooks to configure three EC2 instances for the following tasks:

1. Control Machine (Ansible Control Node)
2. Frontend Machine (Target for NGINX)
3. Docker Machine (Target for Docker & Redis)

Below are the setup instructions and SSH configuration steps for connecting and running the Ansible playbooks on these machines.

---

# Prerequisites

Before proceeding, ensure the following prerequisites are met:

- Three EC2 instances are set up and running on AWS.
- Ansible is installed on the Control Machine using sudo apt install ansible
- SSH access is enabled and properly configured between the Control Machine and the other two machines (Frontend and Docker).

---

## Step 1: Set Up the EC2 Instances

1. Create the EC2 instances:
   - Control Machine: This is the local machine or an EC2 instance that will run Ansible.
   - Frontend Machine: This instance will host the NGINX server.
   - Docker Machine: This instance will run Docker and the Redis container.

2. Obtain the Public IPs:
   - Once the EC2 instances are running, noted down their Public IP addresses. 

---

## Step 2: Set Up SSH Access

### Generate SSH Keys on the Control Machine:

On your Control Machine (the machine from which Ansible will run), generate an SSH key pair by running the following command:

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/ansible_key

chmod 600 ~/.ssh/ansible_key

---


## Step 3:  Copying the public key to the others

### public key to the others and access

Then opened the ansible_key.pub from the directory and copied the public key and then added them to the authorized_keys file in the other two machines.

This allows passwordless SSH login from the Control Machine to the Frontend and Docker machines

on the other machines i run the permissions commands to allow access:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys

After creating the Inventory.ini file 

Then i run the below command to access them and it worked successfully:

```bash

ansible all -i /home/ubuntu/ansible_project/inventory.ini -m ping

