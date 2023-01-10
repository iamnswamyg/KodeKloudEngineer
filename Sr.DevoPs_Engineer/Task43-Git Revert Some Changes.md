The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/ecommerce present on Storage server in Stratos DC. However, they reported an issue with the recent commits being pushed to this repo. They have asked the DevOps team to revert repo HEAD to last commit. Below are more details about the task:
1. In /usr/src/kodekloudrepos/ecommerce git repository, revert the latest commit ( HEAD ) to the previous commit (JFYI the previous commit hash should be with initial commit message ).
2. Use revert ecommerce message (please use all small letters for commit message) for the new revert commit.

```
ssh natasha@ststor01
sudo su -
cd /usr/src/kodekloudrepos/ecommerce/
git status
git log
git revert HEAD //git reset Head~1 will destroy any temperory uncommited changes
git add .
git commit -m " revert ecommerce "
git log
```