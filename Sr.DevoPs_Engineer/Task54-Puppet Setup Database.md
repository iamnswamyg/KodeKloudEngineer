The Nautilus DevOps team had a meeting with development team last week to discuss about some new requirements for an application deployment. Team is working on to setup a mariadb database server on Nautilus DB Server in Stratos Datacenter. They want to setup the same using Puppet. Below you can find more details about the requirements:
1. Create a puppet programming file demo.pp under /etc/puppetlabs/code/environments/production/manifests directory on puppet master node i.e on Jump Server. Define a class mysql_database in puppet programming code and perform below mentioned tasks:
2. Install package mariadb-server (whichever version is available by default in yum repo) on puppet agent node i.e on DB Server also start its service.
3. Create a database kodekloud_db6 , a database user kodekloud_gem and set password 8FmzjvFU6S for this new user also remember host should be localhost. Finally grant some usual permissions like select, update (or full) ect to this newly created user on newly created database.
4. Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

```
sudo su -
cd /etc/puppetlabs/code/environments/production/manifests/
vi demo.pp
[
class mysql_database {
    package {'mariadb-server':
      ensure => installed
    }
    service {'mariadb':
        ensure    => running,
        enable    => true,
    }    
    mysql::db { 'kodekloud_db6':
      user     => 'kodekloud_gem',
      password => '8FmzjvFU6S',
      host     => 'localhost',
      grant    => ['ALL'],
    }
}
node 'stdb01.stratos.xfusioncorp.com' {
  include mysql_database
}  
]
puppet parser validate demo.pp
ssh peter@stdb01
sudo su -
puppet agent -tv
systemctl status mariadb 
mysql -u kodekloud_gem -p kodekloud_db6 -h localhost
```