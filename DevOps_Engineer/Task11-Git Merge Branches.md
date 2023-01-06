The Nautilus application development team has been working on a project repository /opt/games.git. This repo is cloned at /usr/src/kodekloudrepos on storage server in Stratos DC. They recently shared the following requirements with DevOps team:
a. Create a new branch datacenter in /usr/src/kodekloudrepos/games repo from master and copy the /tmp/index.html file (on storage server itself). Add/commit this file in the new branch and merge back that branch to the master branch. Finally, push the changes to origin for both of the branches.

```
ssh natasha@ststor01
sudo su -
ll /usr/src/kodekloudrepos/games/
cd /usr/src/kodekloudrepos/games/
git status
git checkout -b datacenter
git status
git branch
cp /tmp/index.html  /usr/src/kodekloudrepos/games/
ll /usr/src/kodekloudrepos/games/
git add index.html
git commit -m "added index.html"
git checkout master
git merge datacenter
git push -u origin datacenter
git push -u origin master
git status
```
