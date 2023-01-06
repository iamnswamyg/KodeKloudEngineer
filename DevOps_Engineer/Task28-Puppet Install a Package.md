Some new packages need to be installed on app server 3 in Stratos Datacenter. The Nautilus DevOps team has decided to install the same using Puppet. Since jump host is already configured to run as Puppet master server and all app servers are already configured to work as the puppet agent nodes, we need to create required manifests on the Puppet master server so that the same can be applied on all Puppet agent nodes. Please find more details about the task below.
Create a Puppet programming file media.pp under /etc/puppetlabs/code/environments/production/manifests directory on master node i.e Jump Server and using puppet package resource perform the tasks given below.
Install package vsftpd through Puppet package resource only on App server 3i.epuppet agent node 3`.
Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

```
cd /etc/puppetlabs/code/environments/production/manifests/
ll
vi media.pp
[
class vsftpd_installer {
    package {'vsftpd':
        ensure => installed
    }
}
node  'stapp03.stratos.xfusioncorp.com' {
  include vsftpd_installer
}
]
puppet parser validate media.pp
ssh banner@stapp03
sudo su -
puppet agent -tv
rpm -qa |grep vsftpd
```