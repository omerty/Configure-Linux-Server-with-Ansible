# Ansible Linux Server Configuration

This project automates the configuration of a Linux server using Ansible, ensuring the server is secure, optimized, and ready for deployment. The playbook includes tasks such as updating packages, setting up SSH securely, installing essential tools, and configuring a basic firewall.

---

## Features

- **Update and Upgrade Packages**: Keeps the server updated with the latest security patches.
- **Install Essential Software**: Tools like `curl`, `vim`, and `git` are installed.
- **Set Timezone**: Configures the server's timezone to UTC for consistency.
- **Secure SSH**: Disables root login and ensures secure SSH access.
- **Firewall Configuration**: Activates the firewall and allows SSH traffic.

---

## Requirements

- A Linux server (Ubuntu/Debian-based or similar).
- Ansible installed on your control machine.
- SSH access to the target server.
- Optional: `ufw` or `firewalld` for firewall configuration.

---

## Setup

### 1. Install Ansible
Install Ansible on your control machine. For example, on Ubuntu:
  ```bash
  sudo apt update
  sudo apt install ansible

### 2. Clone the Project
  git clone https://github.com/yourusername/ansible-linux-server-config.git
  cd ansible-linux-server-config

### 3. Configure the Inventory
Edit the inventory file to include your servers IP and SSH user:
  git clone https://github.com/yourusername/ansible-linux-server-config.git
  cd ansible-linux-server-config
Replace 127.0.0.1 with your servers IP address and your_user with your SSH username.

### 4. Update the Playbook
Modify configure_server.yml if you need to adjust configurations or add additional tasks.

### 5. Run the Playbook
  ansible-playbook -i inventory configure_server.yml



## Playbook Breakdown
## Update and Upgrade Packages
Ensures all installed packages are up to date:
  yaml
  - name: Update and upgrade packages
    apt:
      update_cache: yes
      upgrade: dist

## Update and Upgrade Packages
Installs essential tools like curl, vim, and git:
  yaml
  - name: Install necessary packages
    apt:
      name:
        - curl
        - vim
        - git
      state: present

## Set Timezone
Configures the servers timezone to UTC:
  yaml
  Copy code
  - name: Set timezone
    timezone:
      name: UTC

## Secure SSH
Disables root login by modifying /etc/ssh/sshd_config:
  yaml
  - name: Secure SSH
    lineinfile:
      path: /etc/ssh/sshd_config
      regexp: '"^""#?PermitRootLogin'
      line: 'PermitRootLogin no'
      state: present

## Configure Firewall
Activates the firewall and ensures SSH traffic is allowed:
  yaml
  - name: Configure firewall
    ufw:
      state: enabled
      rule:
        name: ssh
        action: allow


