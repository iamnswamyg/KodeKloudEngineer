xFusionCorp Industries has planned to set up a common email server in Stork DC. After several meetings and recommendations they have decided to use postfix as their mail transfer agent and dovecot as an IMAP/POP3 server. We would like you to perform the following steps:
Install and configure postfix on Stork DC mail server.
Create an email account john@stratos.xfusioncorp.com identified by ksH85UJjhb.
Set its mail directory to /home/john/Maildir.
Install and configure dovecot on the same server.

```
ssh groot@stmail01
sudo su -
yum install postfix -y
yum install dovecot -y
vi /etc/postfix/main.cf
[
myhostname = stmail01.stratos.xfusioncorp.com
mydomain = stratos.xfusioncorp.com
myorigin = $mydomain
inet_interfaces = all
#inet_interfaces = localhost
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
mynetworks = 172.16.238.0/24, 127.0.0.0/8
home_mailbox = Maildir/
]
cat /etc/postfix/main.cf | grep stmail01.stratos.xfusioncorp.com
cat /etc/postfix/main.cf | grep stratos.xfusioncorp.com
cat /etc/postfix/main.cf | grep myorigin
cat /etc/postfix/main.cf | grep inet_interfaces
cat /etc/postfix/main.cf | grep mydestination
cat /etc/postfix/main.cf | grep mynetworks
cat /etc/postfix/main.cf | grep home_mailbox
systemctl start postfix
systemctl status postfix
useradd john
passwd john
cat /etc/passwd | grep john
ll /home/john
telnet stmail01 25
EHLO localhost
mail from:john@stratos.xfusioncorp.com
rcpt to:john@stratos.xfusioncorp.com
DATA
test mail
.
quit
su - john
mailq
cd Maildir/
ll
cat new/1672676793.V801I3918017M600420.stmail01.stratos.xfusioncorp.com
exit
vi /etc/dovecot/dovecot.conf
[
protocols = imap pop3 lmtp
]
vi /etc/dovecot/conf.d/10-mail.conf
[
mail_location = maildir:~/Maildir
]
vi /etc/dovecot/conf.d/10-auth.conf
[
auth_mechanisms = plain login
]
vi /etc/dovecot/conf.d/10-master.con
[
# permissions (e.g. 0777 allows everyone full permissions).
  unix_listener auth-userdb {
    #mode = 0666
    user = postfix
    group = postfix
  }
]
systemctl start dovecot
systemctl status dovecot
telnet stmail01 110
user john
pass ksH85UJjhb
retr 1
quit
ss -tulnp
```