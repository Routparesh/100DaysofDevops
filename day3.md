### Day-3: Secure SSH Root Access

Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.

Your task is to disable direct SSH root login on all app servers within the Stratos Datacenter.

```bash
sudo nano /etc/ssh/sshd_config
 ### Change/Add: PermitRootLogin no
sudo systemctl restart sshd

```
