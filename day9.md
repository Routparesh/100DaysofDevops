## Day 9: MariaDB Troubleshooting

```bash
> sudo cat /var/log/mariadb/mariadb.log

> sudo chown -R mysql:mysql /var/lib/mysql

> sudo chmod 750 /var/lib/mysql

> sudo restorecon -Rv /var/lib/mysql

> sudo systemctl restart mariadb

> sudo systemctl status mariadb

```
