New packages need to be installed on some of the app servers in Stratos Datacenter. The Nautilus DevOps team has decided to install the same using Puppet. Since jump host is already configured to run as Puppet master server and all app servers are already configured to work as puppet agent nodes, we need to create the required manifests on the Puppet master server so that it can be applied on the required Puppet agent node. Please find more details about the task below.
1. Create a Puppet programming file games.pp under /etc/puppetlabs/code/environments/production/manifests directory on master node i.e Jump Host to perform the below given tasks.
2. Install package vsftpd using puppet package resource and start its service using puppet service resource on Puppet agent node 2 i.e App Server 2.
Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

```
ssh -t steve@stapp02 "systemctl status  vsftpd"
sudo su -
cd /etc/puppetlabs/code/environments/production/manifests
vi games.pp
[
class vsftpd_installer {
    package {'vsftpd':
        ensure => installed
    }
    service {'vsftpd':
        ensure    => running,
        enable    => true,
    }
}
node 'stapp02.stratos.xfusioncorp.com'{
  include vsftpd_installer
}  
]
puppet parser validate games.pp
ssh steve@stapp02
sudo su -
puppet agent -tv
systemctl status vsftpd
```