During the daily standup, it was pointed out that the timezone across Nautilus Application Servers in Stratos Datacenter doesn't match with that of the local datacenter's timezone, which is Africa/Ceuta.
Correct the mismatch.

ssh 172.16.238.10 -l tony
ssh 172.16.238.11 -l steve
ssh 172.16.238.12 -l banner
rm -f /etc/localtime
ln -sf /usr/share/zoneinfo/Africa/Ceuta /etc/localtime
or
sudo timedatectl set-timezone Africa/Ceuta