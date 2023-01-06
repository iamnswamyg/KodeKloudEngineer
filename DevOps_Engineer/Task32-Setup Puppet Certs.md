The Nautilus DevOps team has set up a puppet master and an agent node in Stratos Datacenter. Puppet master is running on jump host itself (also note that Puppet master node is also running as Puppet CA server) and Puppet agent is running on App Server 1. Since it is a fresh set up, the team wants to sign certificates for puppet master as well as puppet agent nodes so that they can proceed with the next steps of set up. You can find more details about the task below:
Puppet server and agent nodes are already have required packages, but you may need to start puppetserver (on master) and puppet service on both nodes.
Assign and sign certificates for both master and agent node.

```
sudo su -
vi /etc/hosts
[
172.16.238.3    jump_host.stratos.xfusioncorp.com jump_host puppet
172.16.239.3    jump_host.stratos.xfusioncorp.com jump_host puppet
172.17.0.5      jump_host.stratos.xfusioncorp.com jump_host puppet
]
systemctl status puppetserver
puppetserver ca list --all

//go to agent
ssh tony@stapp01
vi /etc/hosts
[
172.16.238.3    jump_host.stratos.xfusioncorp.com jump_host puppet
172.16.239.3    jump_host.stratos.xfusioncorp.com jump_host puppet
172.17.0.5      jump_host.stratos.xfusioncorp.com jump_host puppet
]
ping jump_host.stratos.xfusioncorp.com
systemctl status puppet
systemctl restart puppet
systemctl status puppet

//on server
puppetserver ca list --all
puppetserver ca sign --all

//on agent
systemctl restart puppet
puppet agent -t
```