The Nautilus DevOps team has put some data on all app servers in Stratos DC. jump host is configured as Puppet master server, and all app servers are already been configured as Puppet agent nodes. The team needs to update the content of some of the exiting files, as well as need to update their permissions etc. Please find below more details about the task:
1.Create a Puppet programming file official.pp under /etc/puppetlabs/code/environments/production/manifests directory on the master node i.e Jump Server. Using puppet file resource, perform the below mentioned tasks.
2.A file named blog.txt already exists under /opt/data directory on App Server 2.
3.Add content Welcome to xFusionCorp Industries! in blog.txt file on App Server 2.
4.Set its permissions to 0777.
Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

```
sudo su -
vi /etc/puppetlabs/code/environments/production/manifests/official.pp
[
 class file_modifier {
   # Update blog.txt under /opt/data
   file { '/opt/data/blog.txt':
     ensure => 'present',
     content => 'Welcome to xFusionCorp Industries!',
     mode => '0744',
   }
 }
 node 'stapp02.stratos.xfusioncorp.com' {
   include file_modifier
 } 
]
puppet parser validate official.pp
ssh steve@stapp02
sudo su -
puppet agent -tv
cat /opt/data/blog.txt
```