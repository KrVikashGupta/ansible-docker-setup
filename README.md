
# 🤖✨ Ansible Automation Playbooks Guide

![Ansible](https://img.shields.io/badge/Ansible-2.9+-blue?logo=ansible\&style=for-the-badge)
![GitHub](https://img.shields.io/badge/GitHub-Repository-black?logo=github\&style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge) 
![CI/CD](https://img.shields.io/badge/CI-CD-orange?style=for-the-badge)

---

## 📖 Table of Contents

1. [🚀 Introduction](#-introduction)
2. [⚙️ Prerequisites](#-prerequisites)
3. [📂 Project Structure](#-project-structure)
4. [🛠️ Getting Started](#-getting-started)
5. [🎯 Playbooks & Roles](#-playbooks--roles)
6. [💻 Common Ansible Commands](#-common-ansible-commands)
7. [🗂️ Inventory Management](#-inventory-management)
8. [🤖 Automation Examples](#-automation-examples)
9. [📦 Best Practices](#-best-practices)
10. [🐞 Troubleshooting](#-troubleshooting)
11. [📄 License](#-license)

---

## 🚀 Introduction

Ansible is an **open-source IT automation tool** used for:

* ⚡ Automating software provisioning and configuration
* 🖥️ Deploying applications to multiple servers
* 🌐 Orchestrating infrastructure across cloud and on-prem
* 🔄 Managing repetitive tasks efficiently
* 👥 Improving team collaboration

---

## ⚙️ Prerequisites

Before using these playbooks, ensure you have:

* 🛠️ Ansible `v2.9+` installed
* 💻 Linux or Windows Control Node
* 🖥️ SSH access to target servers
* 📂 Proper directory structure for playbooks and roles

---

## 📂 Project Structure

```
ansible-project/
├── inventories/        # 🌍 Hosts and group configurations
│   ├── production/
│   └── staging/
├── playbooks/          # 📝 Main playbooks
│   ├── setup.yml
│   ├── deploy-web.yml
│   └── monitor.yml
├── roles/              # 🎯 Reusable roles
│   ├── common/
│   ├── webserver/
│   └── nagios/
├── group_vars/         # 🔧 Variables per group
├── host_vars/          # 🛠️ Variables per host
└── README.md           # 📖 Documentation
```

---

## 🛠️ Getting Started

1. **Clone the repository:**

```bash
git clone https://github.com/<username>/<repo>.git
cd ansible-project
```

2. **Check Ansible version:**

```bash
ansible --version
```

3. **Test connectivity to hosts:**

```bash
ansible all -m ping -i inventories/production/hosts
```

4. **Run a playbook:**

```bash
ansible-playbook -i inventories/production/hosts playbooks/setup.yml
```

---

## 🎯 Playbooks & Roles

### Playbooks

* `setup.yml` → Installs common packages and configures servers
* `deploy-web.yml` → Deploys web servers and custom pages
* `monitor.yml` → Configures Nagios monitoring

### Roles

* **common** → Installs essential packages (`git`, `vim`, `curl`)
* **webserver** → Installs Apache/Nginx and deploys custom content
* **nagios** → Installs Nagios agent and configures host/service checks

**Example: Using a Role in Playbook**

```yaml
- hosts: webservers
  become: yes
  roles:
    - common
    - webserver
```

---

## 💻 Common Ansible Commands

| Command                                 | Emoji | Description                             |
| --------------------------------------- | ----- | --------------------------------------- |
| `ansible all -m ping`                   | 🏓    | Test connectivity to all hosts          |
| `ansible-playbook playbook.yml`         | 🚀    | Run a playbook                          |
| `ansible-playbook playbook.yml --check` | 🔍    | Dry run / check only                    |
| `ansible-playbook playbook.yml --diff`  | 📝    | Show differences after applying changes |
| `ansible-galaxy install <role>`         | 🎯    | Install external roles from Galaxy      |
| `ansible-doc <module>`                  | 📚    | View module documentation               |
| `ansible-vault create secret.yml`       | 🔒    | Encrypt sensitive data                  |

---

## 🗂️ Inventory Management

**Static Inventory Example:**

```ini
[webservers]
web1 ansible_host=192.168.1.10
web2 ansible_host=192.168.1.11

[dbservers]
db1 ansible_host=192.168.1.20
```

**Dynamic Inventory:**

* Generate inventory automatically from cloud providers (AWS, GCP, Azure)
* Use `ansible-inventory --list -i dynamic_inventory.py` to verify

---

## 🤖 Automation Examples

### 1️⃣ Installing Packages

```yaml
- name: Install essential packages
  hosts: all
  become: yes
  tasks:
    - name: Install git, curl, vim
      apt:
        name: "{{ item }}"
        state: present
      loop:
        - git
        - curl
        - vim
```

### 2️⃣ Deploy Web Server

```yaml
- name: Setup Apache Web Server
  hosts: webservers
  become: yes
  roles:
    - webserver
```

### 3️⃣ Configure Nagios Monitoring

```yaml
- name: Setup Nagios monitoring
  hosts: monitored_hosts
  become: yes
  roles:
    - nagios
```

---

## 📦 Best Practices

* 🌱 Use **roles** to keep playbooks modular
* 🔧 Keep **group_vars** and **host_vars** for configuration
* 🔒 Store secrets using **Ansible Vault**
* 🔄 Use **idempotent tasks** for safe reruns
* 📝 Document your playbooks for clarity

---

## 🐞 Troubleshooting

* `UNREACHABLE!` → Check SSH connectivity and user permissions
* `FAILED! => {"msg": ...}` → Check task syntax and variables
* Module not found → Install via `ansible-galaxy` or update Ansible
* Permissions issues → Use `become: yes` for sudo privileges

---

## 📄 License

MIT License © 2025 🛡️

---

✨ **Automate Everything with Ansible!** 🤖💻💡🌐🚀

---
