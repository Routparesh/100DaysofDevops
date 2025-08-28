## Day 11: Install and Configure Tomcat Server

```bash
> sudo dnf install java-11-openjdk -y

> java -version

> sudo curl -O https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.96/bin/apache-tomcat-9.0.96.tar.gz

> sudo tar -xvzf apache-tomcat-9.0.96.tar.gz

> sudo mv ~/apache-tomcat-9.0.96 /opt/tomcat

> sudo chmod +x /opt/tomcat/bin/*.sh

> sudo chown -R banner:banner /opt/tomcat

```

```bash
> nano /opt/tomcat/conf/server.xml
```

Change Tomcat Port to 6400
Find this section:
<Connector port="8080" protocol="HTTP/1.1"

Change 8080 to 6400:
<Connector port="6400" protocol="HTTP/1.1"

Save & exit.

1️⃣ Find your JDK path

```bash
sudo alternatives --config java
```

1️⃣ Create the systemd service file
On App Server 3:

```bash
sudo nano /etc/systemd/system/tomcat.service
```

Paste this:

```bash
[Unit]
Description=Apache Tomcat Web Application Container
After=network.target
[Service]
Type=forking
User=banner
Group=banner
Environment=JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.20.1.1-2.el9.x86_64
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
Environment=CATALINA_HOME=/opt/tomcat
Environment=CATALINA_BASE=/opt/tomcat
ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh
[Install]
WantedBy=multi-user.target
```

2️⃣ Reload systemd and start Tomcat

```bash
sudo systemctl daemon-reload
sudo systemctl start tomcat
sudo systemctl enable tomcat
sudo systemctl status tomcat
```

Transfer ROOT.war from Jump Host
On the Jump Host:

```bash
> scp /tmp/ROOT.war banner@stapp03:/opt/tomcat/webapps/
```
