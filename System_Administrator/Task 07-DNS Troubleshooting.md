The system admins team of xFusionCorp Industries has noticed intermittent issues with DNS resolution in several apps . App Server 1 in Stratos Datacenter is having some DNS resolution issues, so we want to add some additional DNS nameservers on this server.
As a temporary fix we have decided to go with Google public DNS (ipv4). Please make appropriate changes on this server.

```
ssh tony@172.16.238.10
sudo su -
cat /etc/resolv.conf
vi /etc/resolv.conf

search stratos.xfusioncorp.com
nameserver 127.0.0.11
nameserver 8.8.8.8
options ndots:0
```