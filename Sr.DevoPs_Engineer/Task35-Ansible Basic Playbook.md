One of the Nautilus DevOps team members was working on to test an Ansible playbook on jump host. However, he was only able to create the inventory, and due to other priorities that came in he has to work on other tasks. Please pick up this task from where he left off and complete it. Below are more details about the task:
1. The inventory file /home/thor/ansible/inventory seems to be having some issues, please fix them. The playbook needs to be run on App Server 1 in Stratos DC, so inventory file needs to be updated accordingly.
2. Create a playbook /home/thor/ansible/playbook.yml and add a task to create an empty file /tmp/file.txt on App Server 1.
Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.

```
vi /home/thor/ansible/inventory   
[
stapp01 ansible_host=172.16.238.10 ansible_user=tony ansible_ssh_pass=Ir0nM@n  
]
vi /home/thor/ansible/playbook.yml
[
- name: Create file in appserver
  hosts: stapp01
  become: yes
  tasks:
    - name: Create the file
      file:
        path: /tmp/file.txt
        state: touch  
]
cd /home/thor/ansible
ansible all -a "ls -ltr /tmp/" -i inventory
ansible-playbook -i inventory playbook.yml
ansible all -a "ls -ltr /tmp/" -i inventory
```