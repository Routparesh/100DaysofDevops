## Day 15: Setup SSL for Nginx

The system admins team of xFusionCorp Industries needs to deploy a new application on App Server 1 in Stratos Datacenter. They have some pre-requites to get ready that server for application deployment. Prepare the server as per requirements shared below:

1. Install and configure nginx on App Server 1.
2. On App Server 1 there is a self signed SSL certificate and key present at location /tmp/nautilus.crt and /tmp/nautilus.key. Move them to some appropriate location and deploy the same in Nginx.
3. Create an index.html file with content Welcome! under Nginx document root.
4. For final testing try to access the App Server 1 link (either hostname or IP) from jump host using curl command. For example curl -Ik https://<app-server-ip>/.

```bash

sudo yum install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx

sudo mkdir -p /etc/nginx/ssl
sudo mv /tmp/nautilus.crt /etc/nginx/ssl/
sudo mv /tmp/nautilus.key /etc/nginx/ssl/

sudo chmod 600 /etc/nginx/ssl/nautilus.key
sudo chmod 644 /etc/nginx/ssl/nautilus.crt
sudo vi /etc/nginx/nginx.conf

```

Add:
server {
listen 443 ssl;
server*name *;

    ssl_certificate /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    root /usr/share/nginx/html;
    index index.html;

}

```bash
echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html
sudo nginx -t
sudo systemctl restart nginx
curl -Ik https://<stapp01-ip>/
```
