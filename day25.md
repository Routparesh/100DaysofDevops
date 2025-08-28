## Day 25: Git Merge Branches

The Nautilus application development team has been working on a project repository /opt/blog.git. This repo is cloned at /usr/src/kodekloudrepos on storage server in Stratos DC. They recently shared the following requirements with DevOps team:

Create a new branch devops in /usr/src/kodekloudrepos/blog repo from master and copy the /tmp/index.html file (present on storage server itself) into the repo. Further, add/commit this file in the new branch and merge back that branch into master branch. Finally, push the changes to the origin for both of the branches.

```bash
cd /usr/src/kodekloudrepos/blog
git branch
git checkout -b devops

cd
cp /tmp/index.html /usr/src/kodekloudrepos/blog
ls
git add index.html
git commit -m"add index.html"

git checkout master
git merge devops

git push origin master
git push origin devops
```
