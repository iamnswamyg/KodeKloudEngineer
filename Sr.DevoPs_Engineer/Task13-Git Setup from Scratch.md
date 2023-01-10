Some new developers have joined xFusionCorp Industries and have been assigned Nautilus project. They are going to start development on a new application, and some pre-requisites have been shared with the DevOps team to proceed with. Please note that all tasks need to be performed on storage server in Stratos DC.
a. Install git, set up any values for user.email and user.name globally and create a bare repository /opt/media.git.
b. There is an update hook (to block direct pushes to master branch) under /tmp on storage server itself; use the same to block direct pushes to master branch in /opt/media.git repo.
c. Clone /opt/media.git repo in /usr/src/kodekloudrepos/media directory.
d. Create a new branch xfusioncorp_media in repo that you cloned in /usr/src/kodekloudrepos.
e. There is a readme.md file in /tmp on storage server itself; copy that to repo, add/commit in the new branch you created, and finally push your branch to origin.
f. Also create master branch from your branch and remember you should not be able to push to master as per hook you have set up.

```
ssh natasha@ststor01
sudo su -
yum install -y git
git config --global --add user.name natasha
git config --global --add user.email natasha@stratos.xfusioncorp.com
git init --bare /opt/media.git
cp /tmp/update  /opt/media.git/hooks/
cd /usr/src/kodekloudrepos/
git clone  /opt/media.git
ll
cd media
git checkout -b xfusioncorp_media
cp /tmp/readme.md .
ll
git add readme.md
git commit -m "addeded readme.md file"
git push origin xfusioncorp_media
git checkout -b master
git branch
git push origin master
```