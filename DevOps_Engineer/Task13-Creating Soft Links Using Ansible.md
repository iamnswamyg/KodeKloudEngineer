The Nautilus DevOps team is practicing some of the Ansible modules and creating and testing different Ansible playbooks to accomplish tasks. Recently they started testing an Ansible file module to create soft links on all app servers. Below you can find more details about it.
Write a playbook.yml under /home/thor/ansible directory on jump host, an inventory file is already present under /home/thor/ansible directory on jump host itself. Using this playbook accomplish below given tasks:
Create an empty file /opt/data/blog.txt on app server 1; its user owner and group owner should be tony. Create a symbolic link of source path /opt/data to destination /var/www/html.
Create an empty file /opt/data/story.txt on app server 2; its user owner and group owner should be steve. Create a symbolic link of source path /opt/data to destination /var/www/html.
Create an empty file /opt/data/media.txt on app server 3; its user owner and group owner should be banner. Create a symbolic link of source path /opt/data to destination /var/www/html.
Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way without passing any extra arguments.

```
cd /home/thor/ansible
ll
 ansible all -a "ls -ltr /opt/data" -i inventory
 vi /home/thor/ansible/playbook.yml
 [
- name: Create text files and create soft link
  hosts: stapp01, stapp02, stapp03
  become: yes
  tasks:
    - name: Create the blog.txt on stapp01
      file:
        path: /opt/data/blog.txt
        owner: tony
        group: tony
        state: touch
      when: inventory_hostname == "stapp01"
    - name: Create the story.txt on stapp02
      file:
        path: /opt/data/story.txt
        owner: steve
        group: steve
        state: touch
      when: inventory_hostname == "stapp02"
    - name: Create the media.txt on stapp03
      file:
        path: /opt/data/media.txt
        owner: banner
        group: banner
        state: touch
      when: inventory_hostname == "stapp03"
    - name: Link /opt/data directory
      file:
        src: /opt/data/
        dest: /var/www/html
        state: link

 ]
ansible-playbook  -i inventory playbook.yml
ansible all -a "ls -ltr /opt/data" -i inventory
```