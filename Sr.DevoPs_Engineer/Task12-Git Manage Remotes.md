The xFusionCorp development team added updates to the project that is maintained under /opt/beta.git repo and cloned under /usr/src/kodekloudrepos/beta. Recently some changes were made on Git server that is hosted on Storage server in Stratos DC. The DevOps team added some new Git remotes, so we need to update remote on /usr/src/kodekloudrepos/beta repository as per details mentioned below:
a. In /usr/src/kodekloudrepos/beta repo add a new remote dev_beta and point it to /opt/xfusioncorp_beta.git repository.
b. There is a file /tmp/index.html on same server; copy this file to the repo and add/commit to master branch.
c. Finally push master branch to this new remote origin.

```
ssh natasha@ststor01
sudo su -
cd /usr/src/kodekloudrepos/beta
ll
git status
git remote add dev_beta /opt/xfusioncorp_beta.git
git remote -v
cp /tmp/index.html .
ll
git init
git add .
git commit -m "added index.html"
git push -u dev_beta  master
```