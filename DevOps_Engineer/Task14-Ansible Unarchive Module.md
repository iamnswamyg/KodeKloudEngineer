One of the DevOps team members has created an ZIP archive on jump host in Stratos DC that needs to be extracted and copied over to all app servers in Stratos DC itself. Because this is a routine task, the Nautilus DevOps team has suggested automating it. We can use Ansible since we have been using it for other automation tasks. Below you can find more details about the task:
We have an inventory file under /home/thor/ansible directory on jump host, which should have all the app servers added already.
There is a ZIP archive /usr/src/security/nautilus.zip on jump host.
Create a playbook.yml under /home/thor/ansible/ directory on jump host itself to perform the below given tasks.
Unzip /usr/src/security/nautilus.zip archive in /opt/security/ location on all app servers.
Make sure the extracted data must has the respective sudo user as their user and group owner, i.e tony for app server 1, steve for app server 2, banner for app server 3.
The extracted data permissions must be 0744
Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way, without passing any extra arguments.

```
cd  /home/thor/ansible/
cat inventory
ansible all -a "ls -ltr /opt/security/" -i inventory
ll /usr/src/security/
vi playbook.yml
[
- name: Extract archive
  hosts: stapp01, stapp02, stapp03
  become: yes
  tasks:
    - name: Extract the archive and set the owner/permissions
      unarchive:
        src: /usr/src/security/nautilus.zip
        dest: /opt/security/
        owner: "{{ ansible_user }}"
        group: "{{ ansible_user }}"
        mode: "0744"
]
ansible-playbook  -i inventory playbook.yml
ansible all -a "ls -ltr /opt/security/" -i inventory
```