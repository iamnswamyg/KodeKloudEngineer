The Puppet master and Puppet agent nodes have been set up by the Nautilus DevOps team to perform some testing. In Stratos DC all app servers have been configured as Puppet agent nodes. They want to setup a password less SSH connection between Puppet master and Puppet agent nodes and this task needs to be done using Puppet itself. Below are details about the task:
1.Create a Puppet programming file official.pp under /etc/puppetlabs/code/environments/production/manifests directory on the Puppet master node i.e on Jump Server. Define a class ssh_node1 for agent node 1 i.e App Server 1, ssh_node2 for agent node 2 i.e App Server 2, ssh_node3 for agent node3 i.e App Server 3. You will need to generate a new ssh key for thor user on Jump Server, that needs to be added on all App Servers.
2.Configure a password less SSH connection from puppet master i.e jump host to all App Servers. However, please make sure the key is added to the authorized_keys file of each app's sudo user (i.e tony for App Server 1).
Notes: :- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

```
ssh-keygen -t rsa
cat /home/thor/.ssh/id_rsa.pub //copy key
sudo su -
cd /etc/puppetlabs/code/environments/production/manifests
vi official.pp
[
$public_key =  'AAAAB3NzaC1yc2EAAAADAQABAAABAQCtRaIcz3KxxQP3xw5OG4N2rhH1skIxEtcDDEQ4+HA9JgOzj7fAOyL23Vn4ZcYHSYtd7/KYu2qIAFcTsaCNUF9kJELRNymRQpB/450izw9kmuv4xg/fE8F6x1QXPYstO+p8nYyL7W8ItD5oCb0vEX+qAql8eAm06+wd0y0SpHR6mKuS85f3MCSFv7/DJTmuZxltoOarqTrIti9r2iV1V+U/uFXxf7ZpDCmwiP8H6gYrmLoFbKgGc0i1MZBavoIm9DCuK78lWbAKtgvERtx7k4IqYdcbPCd3N0QTT6gnAeHmN3xbmy+y/KGYkhwdj2/L/d0vjUghtql6KG9vqC0aLTCx'

class ssh_node1 {
   ssh_authorized_key { 'tony@stapp01':
     ensure => present,
     user   => 'tony',
     type   => 'ssh-rsa',
     key    => $public_key,
   }
 }

class ssh_node2 {
   ssh_authorized_key { 'steve@stapp02':
     ensure => present,
     user   => 'steve',
     type   => 'ssh-rsa',
     key    => $public_key,

   }
 }
class ssh_node3 {
   ssh_authorized_key { 'banner@stapp03':
     ensure => present,
     user   => 'banner',
     type   => 'ssh-rsa',
     key    => $public_key,
   }
 }

node stapp01.stratos.xfusioncorp.com {
   include ssh_node1
 }
node stapp02.stratos.xfusioncorp.com {
   include ssh_node2
 }
node stapp03.stratos.xfusioncorp.com {
   include ssh_node3
 }  
]
puppet parser validate official.pp
ssh tony@app01
sudo su -
puppet agent -tv
logout
logout
ssh steve@app02
sudo su -
puppet agent -tv
logout
logout
ssh banner@app03
sudo su -
puppet agent -tv
logout
logout
logout //final logout from sudo on jumphost
ssh tony@stapp01
logout
ssh steve@stapp02
logout
ssh banner@stapp03
logout
```