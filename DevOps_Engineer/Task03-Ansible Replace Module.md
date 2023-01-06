There is some data on all app servers in Stratos DC. The Nautilus development team shared some requirement with the DevOps team to alter some of the data as per recent changes they made. The DevOps team is working to prepare an Ansible playbook to accomplish the same. Below you can find more details about the task.
Write a playbook.yml under /home/thor/ansible on jump host, an inventory is already present under /home/thor/ansible directory on Jump host itself. Perform below given tasks using this playbook:
We have a file /opt/dba/blog.txt on app server 1. Using Ansible replace module replace string xFusionCorp to Nautilus in that file.
We have a file /opt/dba/story.txt on app server 2. Using Ansiblereplace module replace the string Nautilus to KodeKloud in that file.
We have a file /opt/dba/media.txt on app server 3. Using Ansible replace module replace string KodeKloud to xFusionCorp Industries in that file.
Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.

```
cd /home/thor/ansible
ll
cat inventory
vi playbook.yml
[
- name: Ansible replace
  hosts: stapp01,stapp02,stapp03
  become: yes
  tasks:
    - name: blog.txt replacement
      replace:
        path: /opt/dba/blog.txt
        regexp: "xFusionCorp"
        replace: "Nautilus"
      when: inventory_hostname == "stapp01"
    - name: story.txt replacement
      replace:
        path: /opt/dba/story.txt
        regexp: "Nautilus"
        replace: "KodeKloud"
      when: inventory_hostname == "stapp02"
    - name: media.txt replacement
      replace:
        path: /opt/dba/media.txt
        regexp: "KodeKloud"
        replace: "xFusionCorp Industries"
      when: inventory_hostname == "stapp03"
]
ansible-playbook -i inventory playbook.yml
ssh -t tony@stapp01 "cat /opt/dba/blog.txt"
ssh -t steve@stapp02 "cat /opt/dba/story.txt"
```
