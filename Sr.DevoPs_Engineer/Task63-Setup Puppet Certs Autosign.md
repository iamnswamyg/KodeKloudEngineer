During last weekly meeting, the Nautilus DevOps team has decided to use Puppet autosign config to auto sign the certificates for all Puppet agent nodes that they will keep adding under the Puppet master in Stratos DC. The Puppet master and CA servers are currently running on jump host and all three app servers are configured as Puppet agents. To set up autosign configuration on the Puppet master server, some configuration settings must be done. Please find below more details:
1. The Puppet server package is already installed on puppet master i.e jump server and the Puppet agent package is already installed on all App Servers. However, you may need to start the required services on all of these servers.
2. Configure autosign configuration on the Puppet master i.e jump server (by creating an autosign.conf in the puppet configuration directory) and assign the certificates for master node as well as for the all agent nodes. Use the respective host's FDQN to assign the certificates.
3. Use alias puppet (dns_alt_names) for master node and add its entry in /etc/hosts config file on master i.e Jump Server as well as on the all agent nodes i.e App Servers.
Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

```
vi /etc/hosts
[
172.16.238.3    jump_host.stratos.xfusioncorp.com jump_host puppet
172.16.239.5    jump_host.stratos.xfusioncorp.com jump_host puppet
172.17.0.7      jump_host.stratos.xfusioncorp.com jump_host puppet
]
ping puppet
vi /etc/puppetlabs/puppet/autosign.conf
[
jump_host.stratos.xfusioncorp.com
stapp01.stratos.xfusioncorp.com
stapp02.stratos.xfusioncorp.com
stapp03.stratos.xfusioncorp.com  
]
systemctl restart puppetserver
systemctl status puppetserver
puppetserver ca list --all

//for stapp01
ssh tony@stapp01
sudo su -
vi /etc/hosts
[
172.16.238.3    jump_host.stratos.xfusioncorp.com jump_host puppet
172.16.239.5    jump_host.stratos.xfusioncorp.com jump_host puppet
172.17.0.7      jump_host.stratos.xfusioncorp.com jump_host puppet
]
ping puppet
systemctl restart puppet
systemctl status puppet
puppet agent -tv

//for stapp02
ssh steve@stapp02
sudo su -
vi /etc/hosts
[
172.16.238.3    jump_host.stratos.xfusioncorp.com jump_host puppet
172.16.239.5    jump_host.stratos.xfusioncorp.com jump_host puppet
172.17.0.7      jump_host.stratos.xfusioncorp.com jump_host puppet
]
ping puppet
systemctl restart puppet
systemctl status puppet
puppet agent -tv

//for stapp03
ssh banner@stapp03
sudo su -
vi /etc/hosts
[
172.16.238.3    jump_host.stratos.xfusioncorp.com jump_host puppet
172.16.239.5    jump_host.stratos.xfusioncorp.com jump_host puppet
172.17.0.7      jump_host.stratos.xfusioncorp.com jump_host puppet
]
ping puppet
systemctl restart puppet
systemctl status puppet
puppet agent -tv

//on jumphost
puppetserver ca list --all
```