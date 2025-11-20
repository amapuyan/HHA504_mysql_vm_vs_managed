# VM Setup
1. Create the VM instance
- Go to Compute Engine → VM Instances → Create Instance
- OS: Ubuntu 25.10 (or 22.04 LTS if preferred)
- Machine type: e2-micro (or default)
- Allow HTTP/HTTPS not needed, but allow SSH
- Boot the VM.

2. SSH into the VM
- Use the browser SSH client inside GCP.

3. Update packages & install MySQL
```
sudo apt update
sudo apt install mysql-server mysql-client -y
```

4. Log into MYSQL
```
sudo mysql
```

5. Create your MySQL user & grant privileges
- Ran into errors here because of typos ("PRIVILIGES").
- This is the correct command:
```
CREATE USER 'anthonym'@'%' IDENTIFIED BY '******************';
GRANT ALL PRIVILEGES ON *.* TO 'anthonym'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
- Verify user:
```
SELECT user, host FROM mysql.user;
```

6. Create your database
```
CREATE DATABASE assignment4;
SHOW DATABASES;
```

7. Install nano 
- (VM originally only listened on 127.0.0.1 which prevented VS Code from connecting.)
```
sudo apt install nano
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
- Change lines:
- From:
```
bind-address            = 127.0.0.1
mysqlx-bind-address     = 127.0.0.1
```
- To:
```
bind-address            = 0.0.0.0
mysqlx-bind-address     = 0.0.0.0
```
- Save + exit
- CTRL + O → Enter → CTRL + X
- Restart

8. Match .env in vscode
```
VM_DB_HOST=<your VM external IP>
VM_DB_PORT=3306
VM_DB_USER=anthonym
VM_DB_PASS=*****************
VM_DB_NAME=assignment4
```

9. Run and connect
```
python scripts/vm_demo.py
```

10. Back in SSH verify tables
```
sudo mysql
SHOW DATABASES;
USE assignment4;
SHOW TABLES;
SELECT * FROM visits;
```