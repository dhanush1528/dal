# 🚀 Ansible Lab Setup on Windows 10 using WSL2

This guide walks you through setting up **WSL2 + Ubuntu + Ansible** on a Windows 10 system and using Ansible to install and start **NGINX** locally.

---

## ✅ Step 1: Enable WSL & Virtual Machine Platform

Open **PowerShell as Administrator** and run:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

🔁 **Restart your computer** after running the above commands.

---

## ✅ Step 2: Set WSL 2 as Default

After the restart, open PowerShell **(Admin)** again and run:

```powershell
wsl --set-default-version 2
```

---

## ✅ Step 3: Install Ubuntu

1. Open **Microsoft Store**
2. Search for **Ubuntu 22.04 LTS**
3. Click **Install**
4. Launch it after installation and create a user account

---

## ✅ Step 4: Enable Virtualization in BIOS (if needed)

If WSL fails with an error like `0x80370102`, enable virtualization:

1. Restart your PC
2. While it boots, press `DEL`, `F2`, or `Esc` to enter BIOS (varies by system)
3. Find and enable:

   * `Intel VT-x`, `Intel Virtualization`, or `AMD-V`
4. Save and exit BIOS

---

## ✅ Step 5: Install Ansible in Ubuntu

Launch Ubuntu from Start Menu and run:

```bash
sudo apt update
sudo apt install ansible -y
```

---

## ✅ Step 6: Create Ansible Lab Folder

```bash
mkdir ~/ansible-lab
cd ~/ansible-lab
```

---

## ✅ Step 7: Set Up Inventory File

Create a file named `hosts`:

```bash
nano hosts
```

Paste the following:

```ini
[local]
localhost ansible_connection=local
```

Save with `Ctrl + O`, then `Enter`, and exit with `Ctrl + X`.

---

## ✅ Step 8: Create Ansible Playbook to Install NGINX

Create a playbook file:

```bash
nano install_nginx.yml
```

Paste the following YAML:

```yaml
---
- name: Install and start NGINX on localhost
  hosts: local
  become: yes

  tasks:
    - name: Install NGINX
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Ensure NGINX is running
      service:
        name: nginx
        state: started
        enabled: yes
```

Save and exit.

---

## ✅ Step 9: Run the Playbook

Run the Ansible playbook:

```bash
ansible-playbook -i hosts install_nginx.yml
```

---

## ✅ Step 10: Verify

Open your browser and visit:

```
http://localhost
```

You should see the **NGINX Welcome Page** if everything worked correctly 🎉

---

## ✅ Summary

You've now:

* Set up WSL2 and Ubuntu on Windows 10
* Installed Ansible
* Wrote and ran a playbook to install and start NGINX

You're ready to automate more with Ansible!

---



# 🚀 Ansible Lab Setup on Windows 11 with WSL2 + Ubuntu

This guide will help you install WSL2, Ubuntu, Ansible, and create a basic playbook to install and run **NGINX**.

---

## ✅ Step 1: Install WSL and Ubuntu (One Command)

Open **PowerShell as Administrator** and run:

```powershell
wsl --install
```

🔄 This will:

* Enable required Windows features
* Set WSL2 as default
* Download and install Ubuntu (usually 22.04 LTS)
* Prompt you to restart your system

---

## ✅ Step 2: Complete Ubuntu Setup

After restart:

1. Ubuntu will auto-launch
2. It will ask for:

   * A **new UNIX username**
   * A **password**
3. You’ll be logged into Ubuntu shell (ready to use 🧑‍💻)

---

## ✅ Step 3: Update & Install Ansible

Inside the Ubuntu terminal:

```bash
sudo apt update
sudo apt install ansible -y
```

---

## ✅ Step 4: Set Up Ansible Inventory

1. Create a working folder:

```bash
mkdir ~/ansible-lab
cd ~/ansible-lab
```

2. Create an inventory file:

```bash
nano hosts
```

Paste this:

```ini
[local]
localhost ansible_connection=local
```

Save using: `Ctrl + O`, then press `Enter`, then `Ctrl + X`

---

## ✅ Step 5: Write a Playbook to Install NGINX

1. Create the playbook file:

```bash
nano install_nginx.yml
```

2. Paste the following YAML:

```yaml
---
- name: Install and start NGINX on localhost
  hosts: local
  become: yes

  tasks:
    - name: Install NGINX
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Ensure NGINX is running
      service:
        name: nginx
        state: started
        enabled: yes
```

Save and exit.

---

## ✅ Step 6: Run the Playbook

```bash
ansible-playbook -i hosts install_nginx.yml
```

---

## ✅ Step 7: Test in Browser

In Windows, open your browser and go to:

```
http://localhost
```

You should see the **NGINX welcome page** 🟢

---




```
- hosts: all
  tasks:
    - ping:
```
