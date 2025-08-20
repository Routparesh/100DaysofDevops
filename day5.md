### Day-5: SElinux installation and configuration

```bash
sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils

sudo nano /etc/selinux/config
```

Change the line:
SELINUX=enforcing
to:
SELINUX=disabled

```bash
sestatus
```
