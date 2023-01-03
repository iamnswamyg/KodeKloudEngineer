There was some users data copied on Nautilus App Server 1 at /home/usersdata location by the Nautilus production support team in Stratos DC. Later they found that they mistakenly mixed up different user data there. Now they want to filter out some user data and copy it to another location. Find the details below:
On App Server 1 find all files (not directories) owned by user javed inside /home/usersdata directory and copy them all while keeping the folder structure (preserve the directories path) to /news directory.

```
ssh tony@stapp01
sudo su -
ll /home/usersdata/
ll /news/
find /home/usersdata/ -type f -user javed -exec cp --parents {} /news \;
ll /news/home/usersdata/
```
