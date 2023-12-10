```yaml
---
# Playbook Name: Install Nginx
# Description: Ansible playbook to install Nginx on a group of servers

# Define the play
- name: Install Nginx
  hosts: web_servers  # Specify the target group of servers
  become: true  # Run tasks with elevated privileges (sudo)

  # List of tasks to be executed on the target servers
  tasks:
    # Task 1: Update apt package cache
    - name: Update apt package cache
      apt:
        update_cache: yes
      # Explanation: Ensure that the local package cache is updated before installing Nginx.

    # Task 2: Install Nginx
    - name: Install Nginx
      apt:
        name: nginx
        state: present
      # Explanation: Install the Nginx package. 'state: present' ensures that the package is installed.

    # Task 3: Start Nginx service
    - name: Start Nginx service
      service:
        name: nginx
        state: started
        enabled: yes
      # Explanation: Ensure that the Nginx service is started and set to start on boot.
```

Save this playbook in a file, such as `nginx_installation.yaml`, and execute it using the following command:

```bash
ansible-playbook nginx_installation.yaml
```
