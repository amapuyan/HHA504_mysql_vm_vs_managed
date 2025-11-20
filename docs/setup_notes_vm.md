# VM Setup
1. Create a Cloud SQL MySQL Instance
- Go to Cloud SQL → Create Instance → MySQL
- Choose MySQL 8.x (latest version).
- Set an instance name (mine was assignment4).
- Set the root password and remember it.
- Leave most defaults.
- Under Connections → Public IP → Authorized networks, click “Add Network” → “Use my IP”.
- This allows your local machine to connect.
- Create the instance (takes 2–5 mins).

2. Create a SQL user 
- Inside the instance → Users → Add User Account
- Username: anthonym
- Password: ******************
- Host: Allow any host (%)
- Save user.

3. Create the Database
- Instance → Databases → Create Database
- Database name: assignment4
- Save.

4. Give user permissions (fix for access denied issue)
- Open Cloud Shell or your local terminal:
```
gcloud config set project YOUR_PROJECT_ID
gcloud sql connect assignment4 --user=root --quiet
```
- Enter password
```
GRANT ALL PRIVILEGES ON assignment4.* TO 'anthonym'@'%';
FLUSH PRIVILEGES;
```

5. Create .env 
```
MAN_DB_HOST=PUBLIC_IP_OF_CLOUD_SQL
MAN_DB_PORT=3306
MAN_DB_USER=anthonym
MAN_DB_PASS=Secretpassword123!
MAN_DB_NAME=assignment4
```

6. Run in vscode
```
python scripts/managed_demo.py
```

7. Verify 
- Reconnect to SQL
```
gcloud sql connect assignment4 --user=root --quiet
```
```
SHOW DATABASES;
USE assignment4;
SHOW TABLES;
SELECT * FROM visits;
```