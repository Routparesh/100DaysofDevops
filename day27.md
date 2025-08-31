## Day 27: Git Revert Some Changes

The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/demo present on Storage server in Stratos DC. However, they reported an issue with the recent commits being pushed to this repo. They have asked the DevOps team to revert repo HEAD to last commit. Below are more details about the task:

In /usr/src/kodekloudrepos/demo git repository, revert the latest commit ( HEAD ) to the previous commit (JFYI the previous commit hash should be with initial commit message ).

Use revert demo message (please use all small letters for commit message) for the new revert commit.

```bash
git revert -n HEAD && git commit -m "revert demo message"

git log --oneline -1

```

```bash
cd /usr/src/kodekloudrepos/demo

git log --oneline

git revert HEAD

```

🔹 What you should do in nano

Inside nano you’ll see something like:

Revert "Add index.html file"

This reverts commit abcd123.
...

Delete everything and type only this (all lowercase as per task requirement):

```bash
revert demo message

git log --oneline -n 2

```
