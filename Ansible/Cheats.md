

### Ansible Commands Cheat Sheet

**1. Ad-hoc Commands:**

- **Ping:**
  ```bash
  ansible all -m ping
  ```
  
- **Run a Command:**
  ```bash
  ansible all -a "your_command_here"
  ```
  
- **Copy Files:**
  ```bash
  ansible all -m copy -a "src=path/to/local/file dest=path/on/target/server"
  ```

- **Install Package:**
  ```bash
  ansible all -m apt -a "name=package_name state=present"
  ```

**2. Playbook Execution:**

- **Run Playbook:**
  ```bash
  ansible-playbook your_playbook.yaml
  ```

- **Run Playbook with Inventory:**
  ```bash
  ansible-playbook -i your_inventory_file.ini your_playbook.yaml
  ```

- **Run Playbook with Tags:**
  ```bash
  ansible-playbook your_playbook.yaml --tags=your_tag
  ```

- **Run Playbook in Check Mode (Dry Run):**
  ```bash
  ansible-playbook your_playbook.yaml --check
  ```

**3. Inventory Management:**

- **List Hosts in Inventory:**
  ```bash
  ansible-inventory --list
  ```

- **Print Information about Hosts:**
  ```bash
  ansible-inventory -i your_inventory_file.ini --graph
  ```

- **List Hosts with a Specific Pattern:**
  ```bash
  ansible-inventory -i your_inventory_file.ini --list --pattern=your_pattern
  ```

**4. Variables and Facts:**

- **Show All Facts for a Host:**
  ```bash
  ansible your_host -m setup
  ```

- **Display Value of a Variable:**
  ```bash
  ansible your_host -m debug -a "var=your_variable"
  ```

**5. Ansible Galaxy:**

- **Install Role from Galaxy:**
  ```bash
  ansible-galaxy install author_name.role_name
  ```

- **Initiate New Role:**
  ```bash
  ansible-galaxy init your_role_name
  ```
