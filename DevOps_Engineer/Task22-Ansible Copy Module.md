There is data on jump host that needs to be copied on all application servers in Stratos DC. Nautilus DevOps team want to perform this task using Ansible. Perform the task as per details mentioned below:
a. On jump host create an inventory file /home/thor/ansible/inventory and add all application servers as managed nodes.
b. On jump host create a playbook /home/thor/ansible/playbook.yml to copy /usr/src/itadmin/index.html file to all application servers at location /opt/itadmin.
Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.

```
cd  /home/thor/ansible/
ll
vi inventory
[
stapp01 ansible_host=172.16.238.10 ansible_ssh_pass=Ir0nM@n  ansible_user=tony
stapp02 ansible_host=172.16.238.11 ansible_ssh_pass=Am3ric@  ansible_user=steve
stapp03 ansible_host=172.16.238.12 ansible_ssh_pass=BigGr33n  ansible_user=banner
]
ansible all -a "ls -ltr /opt/itadmin" -i inventory
vi playbook.yml
[
- name: Ansible copy
  hosts: stapp01,stapp02,stapp03
  become: yes
  tasks:
    - name: copy index.html to itadmin folder
      copy: src=/usr/src/itadmin/index.html dest=/opt/itadmin
]
ansible-playbook -i inventory playbook.yml
ansible all -a "ls -ltr /opt/itadmin" -i inventory
```
