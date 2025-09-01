## Day 12: Linux Network Services

Our monitoring tool has reported an issue in Stratos Datacenter. One of our app servers has an issue, as its Apache service is not reachable on port 3001 (which is the Apache port). The service itself could be down, the firewall could be at fault, or something else could be causing the issue.

Use tools like telnet, netstat, etc. to find and fix the issue. Also make sure Apache is reachable from the jump host without compromising any security settings.

Once fixed, you can test the same using command curl http://stapp01:3001 command from jump host.

```bash
ssh tony@stapp01
sudo systemctl status httpd
sudo netstat -tulpn | grep :3001
sudo kill -9 <PID>
sudo systemctl start httpd
sudo systemctl enable httpd
sudo iptables -L -n
sudo iptables -I INPUT -p tcp --dport 3001 -j ACCEPT
```

Test from jump host

```bash
curl http://stapp01:3001
```
