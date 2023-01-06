Some directory structure in the Stratos Datacenter needs to be changed, there is a directory that needs to be linked to the default Apache document root. We need to accomplish this task using Puppet, as per the instructions given below:
Create a puppet programming file games.pp under /etc/puppetlabs/code/environments/production/manifests directory on puppet master node i.e on Jump Server. Within that define a class symlink and perform below mentioned tasks:
Create a symbolic link through puppet programming code. The source path should be /opt/finance and destination path should be /var/www/html on Puppet agents 2 i.e on App Servers 2.
Create a blank file blog.txt under /opt/finance directory on puppet agent 2 nodes i.e on App Servers 2.
Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

```
cd /etc/puppetlabs/code/environments/production/manifests
vi games.pp
[
class symlink {
  # First create a symlink to /var/www/html
  file { '/opt/finance':
    ensure => 'link',
    target => '/var/www/html',
  }
   # Now create blog.txt under /opt/finance
  file { '/opt/finance/blog.txt':
    ensure => 'present',
  }
}
node 'stapp02.stratos.xfusioncorp.com'{
  include symlink
}
]
puppet parser validate games.pp
ssh steve@stapp02
sudo su -
puppet status
puppet agent -tv
ll /var/www/html/
ll /opt/finance
```