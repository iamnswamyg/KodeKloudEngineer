Nautilus developers are actively working on one of the project repositories, /usr/src/kodekloudrepos/games. They recently decided to implement some new features in the application, and they want to maintain those new changes in a separate branch. Below are the requirements that have been shared with the DevOps team:
1. On Storage server in Stratos DC create a new branch xfusioncorp_games from master branch in /usr/src/kodekloudrepos/games git repo.
Please do not try to make any changes in code.

```
ssh natasha@ststor01
sudo su -
cd /usr/src/kodekloudrepos/games
git branch
git checkout master
git checkout -b xfusioncorp_games
```