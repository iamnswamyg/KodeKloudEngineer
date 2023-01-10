The Puppet master and Puppet agent nodes have been set up by the Nautilus DevOps team so they can perform testing. In Stratos DC all app servers have been configured as Puppet agent nodes. Below are details about the testing scenario they want to proceed with.
Use Puppet file resource and perform the below given task:
2.Create a Puppet programming file official.pp under /etc/puppetlabs/code/environments/production/manifests directory on master node i.e Jump Server.
3.Using /etc/puppetlabs/code/environments/production/manifests/official.pp create a file ecommerce.txt under /opt/sysops directory on App Server 3.
4.Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

```
sudo su -
cd /etc/puppetlabs/code/environments/production/manifests/
vi official.pp
[
class file_creator {
  # Now create ecommerce.txt under /opt/sysops
  file { '/opt/sysops/ecommerce.txt':
    ensure => 'present',
  }
}
 node 'stapp03.stratos.xfusioncorp.com' {
  include file_creator
}
]
puppet parser validate official.pp
ssh banner@stapp03  
sudo su -
puppet agent -tv
ll /opt/sysops/
```