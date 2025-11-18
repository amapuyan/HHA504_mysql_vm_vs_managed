# HHA504_mysql_vm_vs_managed
## Recording : 
### Part 1: https://www.loom.com/share/b68781359e3f4285a981aa0381923fb7
### Part 2: https://www.loom.com/share/726bbed9c2d144929f14c0943e02113f

## Overview
This project compares two deployment options for MySQL using Google Cloud Platform.

1. VM service - GCP: Compute Engine

2. Managed service - GCP: Cloud SQL for MySQL 

## Region Chosen
Compute Engine: us-central-c
Cloud SQL: us-central1 (Iowa)

## Steps to Reproduce
### VM (self-managed MYSQL)
1. Create a Compute Engine VM (Ubuntu)
2. Allow port 3306 in VM firewall
3. Install MySQL Server (sudo apt install mysql-server)
4. Set bind-address = 0.0.0.0
5. Restart MySQL and confirm ports open
6. Create a MySQL user with @'%'
7. Run vm.demo.py to connect database 

### Managed MySQL
1. Create a Cloud SQL MySQL instance
2. Create Cloud SQL user (anthonym)
3. Add Authorized Network for your public IP
4. Connect using gcloud sql connect
5. GRANT ALL PRIVILEGES ON assignment4.* TO 'anthonym'@'%';
6. Run Python script using SQLAlchemy:
7. Create DB
8. Create table
9. Insert rows
10. Read back row count

## Connection String patterns (NO SECRETS)
### VM (self-managed MYSQL)
```
mysql+pymysql://anthonym:*****@34.63.66.209:3306
```
### Managed MySQL
```
mysql+pymysql://anthonym:*****@34.61.117.69:3306
```
