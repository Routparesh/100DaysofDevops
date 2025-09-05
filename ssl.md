We have successfully generated the Certificate Signing Request (CSR). The next step is to send it to a Certificate Authority (CA) for signing. However, since there is no CA available for this lab, we will proceed to create our own self-signed certificate.

On the app01 server, create a self-signed certificate located at /etc/httpd/certs/app01.crt. The corresponding key should be named app01.key. Please use the required details provided below when creating the certificate.

a. Country Name = SG

b. State or Province Name = Capital Tower

c. Locality Name = CT

d. Organization Name = KodeKloud

e. Organizational Unit Name = Education

f. Common Name = app01.com

g. Email Address = admin@kodekloud.com

```bash
sudo openssl req -new -newkey rsa:2048 -nodes -keyout app01.key -out app01.csr
```

```bash
sudo openssl x509 -req -days 3650 -in /etc/httpd/csr/app01.csr -signkey /etc/httpd/csr/app01.key -out app01.crt
```

```bash
/etc/httpd/conf.d/ssl.conf
```

Certificate and key paths:

Certificate: /etc/httpd/certs/app01.crt
Key: /etc/httpd/certs/app01.key

You will update these in the /etc/httpd/conf.d/ssl.conf file by modifying the following properties:

SSLCertificateFile
SSLCertificateKeyFile
After updating, restart Apache to apply your configuration changes.

```bash
echo | openssl s_client -showcerts -servername app01.com -connect app01:443 2>/dev/null | openssl x509 -inform pem
```
