# Ansible Automation - Web Server Deployment

## Overview
This project automates the deployment of an Apache HTTPD web server on a RHEL 9 EC2 instance using Ansible roles, Jinja2 templates, and idempotent playbooks.

## # Ansible Automation — Web Server Deployment

## Overview
This project automates the deployment and configuration of an Apache 
HTTPD web server on a RHEL 9 EC2 instance using Ansible roles, 
Jinja2 templates, and idempotent playbooks.

## Environment
- Cloud: AWS EC2 (t3.small)
- OS: Red Hat Enterprise Linux 9
- Ansible: Installed via pip3
- Architecture: x86_64
- Control Node Hostname: ansible-control

## Project Structure
ansible-automation-ec2/
├── ansible.cfg
├── inventory/
│   └── hosts.ini
├── roles/
│   └── webserver/
│       ├── tasks/
│       │   └── main.yml
│       ├── handlers/
│       │   └── main.yml
│       └── templates/
│           └── httpd.conf.j2
└── playbooks/
    └── deploy_webserver.yml

## Prerequisites
- AWS EC2 instance running RHEL 9
- Python3 and pip3 installed
- Ansible installed via pip3
- Port 80 open in EC2 security group

## How to Run

# Test connectivity
ansible all -m ping

# Deploy the web server
ansible-playbook playbooks/deploy_webserver.yml

# Verify Apache is running
sudo systemctl status httpd

# Verify Apache is serving
curl http://127.0.0.1 (output should be in HTML)

## What Each File Does
- ansible.cfg — global Ansible configuration and behavior
- inventory/hosts.ini — defines target servers and connection vars
- roles/webserver/tasks/main.yml — installs and configures Apache
- roles/webserver/handlers/main.yml — restarts Apache only when triggered
- roles/webserver/templates/httpd.conf.j2 — dynamic Jinja2 config file
- playbooks/deploy_webserver.yml — ties the entire role together

## Key Concepts Demonstrated
- Ansible roles and playbooks
- Idempotent configuration management
- Jinja2 templating for dynamic configs
- Privilege escalation with become: true
- Handler-driven service restarts
- EC2 security groups as firewall replacement

## Troubleshooting challenges
- RHEL subscription required to access DNF repos — registered via
  Red Hat Developer account
- Ansible not in default RHEL repos — installed via pip3
- Firewalld not installed on EC2 — removed task and relied on
  EC2 security group for port 80
- Git ownership conflict from using sudo — fixed with chown and
  safe.directory config

## Idempotency Proof
Running the playbook a second time returns changed=0 confirming
the system was already in the desired state and no unnecessary
changes were made.

## RHCE Portfolio Series
This is Project 1 of 4 built while preparing for my RHCE 
certification (target: June 2026)
