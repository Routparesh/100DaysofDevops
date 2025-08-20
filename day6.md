### Day-6: Create a Cron Job(cent os)

```bash
sudo dnf install cronie -y

crontab -e

*/5 * * * * echo hello > /tmp/cron_text

```
