## Day 22: Clone Git Repository on Storage Server

The DevOps team established a new Git repository last week, which remains unused at present. However, the Nautilus application development team now requires a copy of this repository on the Storage Server in the Stratos DC. Follow the provided details to clone the repository:

The repository to be cloned is located at /opt/demo.git

Clone this Git repository to the /usr/src/kodekloudrepos directory. Ensure no modifications are made to the repository during the cloning process.

```bash
ssh natasha@ststor01

cd /usr/src/kodekloudrepos

sudo git clone /opt/demo.git
```
