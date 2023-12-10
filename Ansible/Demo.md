### Master Machine Setup

#### Install Ansible
```bash
sudo apt-get update
sudo apt install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
```

#### Generating Master Key
```bash
cd 
cd .ssh
ssh-keygen     #generates public and private key
cat rsa.pub    #copy public key

```

#### Connecting Slave in Slave Machine
```bash
cd .ssh
ls
vi authorized-keys
#append copied rsa.pub in this file
```

#### Verify Connection in Master
```bash
ssh ubuntu@<slave_public_ip>
# If successful, exit to the master machine
exit
```

#### Ansible Configuration
```bash
cd /etc/ansible
sudo vi hosts
# Add the following line at the end
# [group]
# slave_name ansible_ssh_host=<slave_public_ip> or <slave_public_ip>
```

#### Test Ansible Ping
```bash
ansible -m ping group
```

#### Create Ansible Playbook
```bash
sudo mkdir playbooks
cd playbooks
sudo vi play.yaml
# Update hosts: group in the playbook
# Add desired tasks in the playbook
```

#### Run Ansible Playbook
```bash
ansible-playbook play.yaml
```
