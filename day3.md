### Day-3: Secure SSH Root Access

```bash
sudo nano /etc/ssh/sshd_config
 ### Change/Add: PermitRootLogin no
sudo systemctl restart sshd

```
