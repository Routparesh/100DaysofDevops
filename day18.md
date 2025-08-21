## Day 18: Configure LAMP server

xFusionCorp Industries is planning to host a WordPress website on their infra in Stratos Datacenter. They have already done infrastructure configuration—for example, on the storage server they already have a shared directory /vaw/www/html that is mounted on each app host under /var/www/html directory. Please perform the following steps to accomplish the task:

a. Install httpd, php and its dependencies on all app hosts.

b. Apache should serve on port 8087 within the apps.

c. Install/Configure MariaDB server on DB Server.

d. Create a database named kodekloud_db8 and create a database user named kodekloud_joy identified as password dCV3szSGNA. Further make sure this newly created user is able to perform all operation on the database you created.

e. Finally you should be able to access the website on LBR link, by clicking on the App button on the top bar. You should see a message like App is able to connect to the database using user kodekloud_joy

```bash

sudo yum install httpd -y
sudo yum install php php-mysqlnd php-gd php-xml php-mbstring php-json -y
sudo yum install nano -y
sudo nano /etc/httpd/conf/httpd.conf
```

Look for the line:
Listen 80
Change it to:
Listen 8087

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
sudo ss -tulnp | grep httpd
sudo systemctl status httpd
```

### In DB Server

```bash
sudo yum install mariadb-server -y
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

```bash
sudo mysql -u root -p
```

```bash

CREATE DATABASE kodekloud_db8;
CREATE USER 'kodekloud_joy' IDENTIFIED BY 'dCV3szSGNA';
GRANT ALL PRIVILEGES ON kodekloud_db8.\* TO 'kodekloud_joy';
FLUSH PRIVILEGES;

```
