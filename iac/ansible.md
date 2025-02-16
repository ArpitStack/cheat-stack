# Ansible IaC Cheatsheet

A comprehensive guide covering essential Ansible commands and configurations for infrastructure automation.

## Table of Contents

- [Installation & Setup](#installation--setup)
- [Inventory Management](#inventory-management)
- [Ad-Hoc Commands](#ad-hoc-commands)
- [Playbooks](#playbooks)
- [Variables & Facts](#variables--facts)
- [Roles & Modules](#roles--modules)
- [Conditionals & Loops](#conditionals--loops)
- [Templates (Jinja2)](#templates-jinja2)
- [Handlers & Notifications](#handlers--notifications)
- [Vault (Secrets Management)](#vault-secrets-management)
- [Ansible Galaxy](#ansible-galaxy)
- [Troubleshooting & Debugging](#troubleshooting--debugging)

## Installation & Setup

Install Ansible:

```bash
sudo apt update && sudo apt install ansible -y
```

Check installed version:

```bash
ansible --version
```

Verify configuration:

```bash
ansible-config dump --only-changed
```

## Inventory Management

Define hosts in `/etc/ansible/hosts`:

```ini
[web]
web1 ansible_host=192.168.1.10
web2 ansible_host=192.168.1.11

[database]
db1 ansible_host=192.168.1.20
```

Test connectivity:

```bash
ansible all -m ping
```

## Ad-Hoc Commands

Run a command on all hosts:

```bash
ansible all -a "uptime"
```

Execute with privilege escalation:

```bash
ansible all -b -m apt -a "name=nginx state=present"
```

Copy a file to remote hosts:

```bash
ansible all -m copy -a "src=/local/file dest=/remote/path"
```

## Playbooks

Basic playbook example:

```yaml
- name: Install Nginx
  hosts: web
  become: true
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
```

Run the playbook:

```bash
ansible-playbook playbook.yml
```

## Variables & Facts

Define variables in playbooks:

```yaml
vars:
  package_name: nginx
```

Use Ansible facts:

```yaml
- debug:
    msg: "The OS is {{ ansible_distribution }}"
```

## Roles & Modules

Create a new role:

```bash
ansible-galaxy init my_role
```

Using a role in a playbook:

```yaml
- hosts: web
  roles:
    - my_role
```

List available modules:

```bash
ansible-doc -l
```

## Conditionals & Loops

Use conditionals:

```yaml
- name: Install on Ubuntu
  apt:
    name: nginx
  when: ansible_os_family == "Debian"
```

Loop through a list:

```yaml
- name: Create multiple users
  user:
    name: "{{ item }}"
    state: present
  loop:
    - alice
    - bob
```

## Templates (Jinja2)

Create a template `nginx.conf.j2`:

```nginx
server {
    listen 80;
    server_name {{ server_name }};
}
```

Use it in a playbook:

```yaml
- name: Deploy Nginx config
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
```

## Handlers & Notifications

Define a handler:

```yaml
- name: Restart Nginx
  service:
    name: nginx
    state: restarted
```

Trigger a handler:

```yaml
- name: Deploy config
  copy:
    src: nginx.conf
    dest: /etc/nginx/nginx.conf
  notify: Restart Nginx
```

## Vault (Secrets Management)

Encrypt a file:

```bash
ansible-vault encrypt secrets.yml
```

Decrypt a file:

```bash
ansible-vault decrypt secrets.yml
```

Edit an encrypted file:

```bash
ansible-vault edit secrets.yml
```

Run a playbook with Vault:

```bash
ansible-playbook playbook.yml --ask-vault-pass
```

## Ansible Galaxy

Search for roles:

```bash
ansible-galaxy search nginx
```

Install a role:

```bash
ansible-galaxy install geerlingguy.nginx
```

## Troubleshooting & Debugging

Enable verbose mode:

```bash
ansible-playbook playbook.yml -vvv
```

Check syntax:

```bash
ansible-playbook playbook.yml --syntax-check
```

List available tasks:

```bash
ansible-playbook playbook.yml --list-tasks
```

Debugging variables:

```yaml
- debug:
    var: ansible_facts
```