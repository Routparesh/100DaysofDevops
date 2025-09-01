## Day 17: Install and Configure PostgreSQL

The Nautilus application development team has shared that they are planning to deploy one newly developed application on Nautilus infra in Stratos DC. The application uses PostgreSQL database, so as a pre-requisite we need to set up PostgreSQL database server as per requirements shared below:

PostgreSQL database server is already installed on the Nautilus database server.
a. Create a database user kodekloud_tim and set its password to BruCStnMT5.
b. Create a database kodekloud_db9 and grant full permissions to user kodekloud_tim on this database.
Note: Please do not try to restart PostgreSQL server service.

```bash
sudo -u postgres psql
CREATE USER kodekloud_tim WITH PASSWORD 'BruCStnMT5';
CREATE DATABASE kodekloud_db9;
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db9 TO kodekloud_tim;
```
