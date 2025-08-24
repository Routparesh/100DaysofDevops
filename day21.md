## Day 21: Set Up Git Repository on Storage Server

The Nautilus development team has provided requirements to the DevOps team for a new application development project, specifically requesting the establishment of a Git repository. Follow the instructions below to create the Git repository on the Storage server in the Stratos DC:

Utilize yum to install the git package on the Storage Server.

Create a bare repository named /opt/news.git (ensure exact name usage).

```bash
ssh natasha@ststor01

sudo yum install git -y

sudo cd /opt

sudo mkdir news.git

sudo cd news.git

sudo git init --bare
```
