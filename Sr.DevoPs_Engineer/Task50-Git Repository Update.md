The Nautilus development team started with new project development. They have created different Git repositories to manage respective project's source code. One of the repo /opt/ecommerce.git was created recently. The team has given us a sample index.html file that is currently present on jump host under /tmp. The repository has been cloned at /usr/src/kodekloudrepos on storage server in Stratos DC.
1. Copy sample index.html file from jump host to storage server under cloned repository at /usr/src/kodekloudrepos, add/commit the file and push to master branch.

```
sudo scp /tmp/index.html  natasha@ststor01:/tmp/
ssh natasha@ststor01
sudo su -
ls /usr/src/kodekloudrepos
cp /tmp/index.html /usr/src/kodekloudrepos/ecommerce/
cd /usr/src/kodekloudrepos/ecommerce/
git status
git add .
git commit -m "add index.html"
git push origin master
```
