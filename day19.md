## Day 19: Install and Configure Web Application

xFusionCorp Industries is planning to host two static websites on their infra in Stratos Datacenter. The development of these websites is still in-progress, but we want to get the servers ready. Please perform the following steps to accomplish the task:

a. Install httpd package and dependencies on app server 3.

b. Apache should serve on port 3000.

c. There are two website's backups /home/thor/ecommerce and /home/thor/games on jump_host. Set them up on Apache in a way that ecommerce should work on the link http://localhost:3000/ecommerce/ and games should work on link http://localhost:3000/games/ on the mentioned app server.

d. Once configured you should be able to access the website using curl command on the respective app server, i.e curl http://localhost:3000/ecommerce/ and curl http://localhost:3000/games/

### In Jump Server

```bash
scp -r /home/thor/ecommerce banner@stapp03:/tmp/
scp -r /home/thor/games banner@stapp03:/tmp/
```

```bash
ssh banner@stapp03

sudo yum install httpd -y
sudo nano /etc/httpd/conf/httpd.conf
```

Look for the line:
Listen 80

Change it to:
Listen 3000

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

```bash
sudo mkdir -p /var/www/html/ecommerce
sudo mkdir -p /var/www/html/games
sudo chown -R apache:apache /var/www/html/ecommerce /var/www/html/games

```

### In App 3

```bash
sudo mv /tmp/ecommerce/* /var/www/html/ecommerce/
sudo mv /tmp/games/* /var/www/html/games/
sudo systemctl restart httpd
```

### verify

```bash
http://localhost:3000/ecommerce/
http://localhost:3000/games/
```
