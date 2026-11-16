# Install MySQL on a Remote Server Using Ansible

## Prerequisites
* **AWS Account** (to launch an EC2 instance)
* **Ansible** installed on your local/control machine

---

## Setup & Installation

### 1. Install the Ansible MySQL Collection
Run the following command on your Ansible control node to install the required MySQL modules:
```bash
ansible-galaxy collection install ansible.mysql
```
### 2. Launch an AWS EC2 Instance
* Launch an **Ubuntu** EC2 instance on AWS.
* Configure the Security Group to allow inbound **SSH (port 22)** traffic.
* Generate and download a **Key Pair** (`.pem` file).

### 3. Update Key Permissions
Restrict the permissions of your private key file so SSH can use it securely:
```bash
chmod 400 <key_name>.pem
```
### 4. Create `ansible.cfg` file inside ansible folder
```ini
[defaults]
inventory =  <inventory.ini file path>
roles_path = ./roles
host_key_checking = true/false
```
### 5. Configure the Ansible Inventory File
+ Filename: `inventory.ini`
+ Add your EC2 instance's public IP address, default username (`ubuntu`), and the path to your `.pem` key file in your `inventory.ini` file:
```ini
[db_servers]
<EC2_PUBLIC_IP> ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/<key_name>.pem
```

### 6 Run the Ansible Playbook
Execute the playbook to install and configure MySQL on the remote server:
```bash
ansible-playbook ./playbooks/main.yml
```

---

## Manual Verification on the EC2 Instance

Connect to your EC2 instance via SSH to verify that MySQL and your system users were configured properly:
```bash
ssh -i <key_name>.pem ubuntu@<EC2_PUBLIC_IP>
```

### 1. Check MySQL Installation
Verify the installed MySQL version and switch to the root user if needed:
```bash
mysql --version
sudo su -
```

### 2. Connect to MySQL and Verify Database
Log into the MySQL shell (enter the password `root` when prompted):
```bash
mysql -u root -p
```

Run the following SQL commands to check your database and tables:
```sql
SHOW DATABASES;
USE einfochips-intern;
SHOW TABLES;
SELECT * FROM users;
EXIT;
```

### 3. Verify System Users
Check the `/home` directory to confirm that the expected system users were created:
```bash
cd /home
ls
```
