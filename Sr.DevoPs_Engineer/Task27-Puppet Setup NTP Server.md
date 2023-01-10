While troubleshooting one of the issues on app servers in Stratos Datacenter DevOps team identified the root cause that the time isn't synchronized properly among the all app servers which causes issues sometimes. So team has decided to use a specific time server for all app servers, so that they all remain in sync. This task needs to be done using Puppet so as per details mentioned below please compete the task:
1. Create a puppet programming file apps.pp under /etc/puppetlabs/code/environments/production/manifests directory on puppet master node i.e on Jump Server. Within the programming file define a custom class ntpconfig to install and configure ntp server on app server 3.
2. Add NTP Server server 3.south-america.pool.ntp.org in default configuration file on app server 3, also remember to use iburst option for faster synchronization at startup.
Please note that do not try to start/restart/stop ntp service, as we already have a scheduled restart for this service tonight and we don't want these changes to be applied right now.
Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

```
sudo su -
puppet module list
puppet module install puppetlabs-ntp
puppet module list
cd /etc/puppetlabs/code/environments/production/manifests/
vi apps.pp
[
class { 'ntp':
  servers => [ '3.south-america.pool.ntp.org iburst' ],                                               
}    
class ntpconfig {
  include ntp
}  
node 'stapp03.stratos.xfusioncorp.com' {
  include ntpconfig
}
]
puppet parser validate apps.pp
ssh banner@stapp03
sudo su -
puppet resource service ntpd
puppet agent -tv
puppet resource service ntpd
```