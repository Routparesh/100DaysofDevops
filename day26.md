## Day 26: Git Manage Remotes

The xFusionCorp development team added updates to the project that is maintained under /opt/media.git repo and cloned under /usr/src/kodekloudrepos/media. Recently some changes were made on Git server that is hosted on Storage server in Stratos DC. The DevOps team added some new Git remotes, so we need to update remote on /usr/src/kodekloudrepos/media repository as per details mentioned below:

a. In /usr/src/kodekloudrepos/media repo add a new remote dev_media and point it to /opt/xfusioncorp_media.git repository.

b. There is a file /tmp/index.html on same server; copy this file to the repo and add/commit to master branch.

c. Finally push master branch to this new remote origin.

```bash
cd /usr/src/kodekloudrepos/media
git remote -v
git add dev_media /opt/xfusioncorp_media.git
cp /tmp/index.html .
git add .
git commit -m"add index.html"
git push dev_media master

```
