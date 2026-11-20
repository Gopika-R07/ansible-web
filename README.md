
# Exercise 6 - Create an Ansible Playbook for a Simple Web Application Infrastructure

## Aim
To create an Ansible playbook for a simple web application infrastructure.

## Requirements
- Ubuntu Linux
- Ansible
- Apache web server
- Terminal

## Procedure

### Step 1: Create the project directory

```bash
mkdir -p ~/ansible-webapp
cd ~/ansible-webapp
```

### Step 2: Create the playbook

```bash
nano webapp.yml
```

Copy the webapp.yml content from YAML_FILES.md.

Save:
- Ctrl + O
- Enter
- Ctrl + X

### Step 3: Install Ansible

If Ansible is not installed:

```bash
sudo apt update
sudo apt install ansible -y
```

Verify:

```bash
ansible --version
```

### Step 4: Execute the playbook

```bash
ansible-playbook webapp.yml --ask-become-pass
```

Enter your Ubuntu sudo password when prompted.

The playbook performs:
1. Installs Apache.
2. Starts and enables Apache.
3. Deploys the HTML web page.
4. Verifies the HTTP response.
5. Displays deployment status.

### Step 5: Verify Apache service

```bash
sudo systemctl status apache2
```

Expected:

active (running)

### Step 6: Verify using terminal

```bash
curl http://localhost
```

Expected HTML content includes:

Hello from Ansible!

My web application was deployed automatically.

### Step 7: Verify using browser

Open:

http://localhost

The deployed web page should appear.

## Expected Result

Apache is installed and running.
The HTML page is deployed successfully.
The HTTP request returns status code 200.

## Result

Thus, an Ansible playbook was created and executed
successfully to deploy a simple web application infrastructure.
```

## GitHub structure

```text
Ansible-WebApp-Exercise6/
│
├── YAML_FILES.md
└── README.md
```

## Practical execution commands

Run these in your Ubuntu terminal:

```bash
mkdir -p ~/ansible-webapp
cd ~/ansible-webapp
nano webapp.yml
```

Paste the YAML from `YAML_FILES.md`, save it, and run:

```bash
ansible-playbook webapp.yml --ask-become-pass
```

Verify:

```bash
sudo systemctl status apache2
curl http://localhost
```

Open `http://localhost` in your browser.

The source PDF gives the playbook command and verification steps on pages 1–3. The YAML indentation above is arranged as valid Ansible syntax while retaining the tasks and HTML content from the PDF. <FileCite ref_id="turn5file0"/>

---

# Experiment 8 – Install Ansible and Configure Ansible Roles

<badge color="success">Repository 2</badge>

Repository name: `Ansible-Roles-Exercise8`

## File 1: `YAML_FILES.md`

This file contains all four YAML files, separated by their actual Ubuntu paths.

### YAML 1 – `prerequisites/tasks/main.yml`

<CodeBlock language="yaml" editable>
---
# tasks file for prerequisites

- name: Install git
  apt:
    name: git
    state: present
    update_cache: yes
