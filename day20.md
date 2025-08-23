## Day 20: Configure Nginx + PHP-FPM Using Unix Sock

The Nautilus application development team is planning to launch a new PHP-based application, which they want to deploy on Nautilus infra in Stratos DC. The development team had a meeting with the production support team and they have shared some requirements regarding the infrastructure. Below are the requirements they shared:

a. Install nginx on app server 2 , configure it to use port 8096 and its document root should be /var/www/html.

b. Install php-fpm version 8.1 on app server 2, it must use the unix socket /var/run/php-fpm/default.sock (create the parent directories if don't exist).

c. Configure php-fpm and nginx to work together.

d. Once configured correctly, you can test the website using curl http://stapp02:8096/index.php command from jump host.

```bash
ssh steve@stapp02
sudo yum install epel-release -y
sudo yum install nginx -y
```

```bash
sudo vi /etc/nginx/nginx.conf
```

Add/update

```bash
server {
    listen 8096;

    root /var/www/html;
    index index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/var/run/php-fpm/default.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}

```

### b. Install PHP-FPM 8.1

```bash
sudo yum install -y php php-cli php-common php-fpm
```

On Ubuntu/Debian:

```bash
sudo apt-get install -y php8.1-fpm
```

### c. Configure PHP-FPM to use unix socket

Edit the pool config:

CentOS/RHEL:

```bash
sudo vi /etc/php-fpm.d/www.conf
```

Ubuntu/Debian:

```bash
sudo vi /etc/php/8.1/fpm/pool.d/www.conf
```

Change these lines:

```bash
listen = /var/run/php-fpm/default.sock
listen.owner = nginx
listen.group = nginx
listen.mode = 0660
```

Make sure socket directory exists:

```bash
sudo mkdir -p /var/run/php-fpm
sudo chown nginx:nginx /var/run/php-fpm   # CentOS/RHEL
# or
sudo chown www-data:www-data /var/run/php-fpm   # Ubuntu/Debian
```

d. Restart services

```bash
# CentOS/RHEL
sudo systemctl enable php-fpm nginx
sudo systemctl restart php-fpm nginx

# Ubuntu/Debian
sudo systemctl enable php8.1-fpm nginx
sudo systemctl restart php8.1-fpm nginx
```

From jump host:

```bash
curl http://stapp02:8096/index.php
```
