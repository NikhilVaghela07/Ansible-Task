## First Install
```
ansible-galaxy collection install ansible.mysql
```

### Create EC2 instance Ubuntu Machine with and allow SSH AND Generate Key Pair.

### In Inventory File add user EC2 machine username, and EC2 public IP, and paste your key pair path.

```
chmod 400 <key_name>.pem
```

### Run this Command:
```
ansible-playbook -i inventory main.yml
```

### For Verfication Configuration install or not. Connect EC2 install SSH:
```
mysql --version
sudo su -
```


# Connect to Mysql-serverEnter password 
```
mysql -u root -p
```

```
root
```

```
SHOW databases;
```
```
USE einfochips-intern;
```
```
SHOW tables;
```
```
SELECT * FROM users;
```
```
exit
```

### Check Users Created or not

```
cd /home
ls
```