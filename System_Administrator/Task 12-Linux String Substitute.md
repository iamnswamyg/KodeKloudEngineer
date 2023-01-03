The backup server in the Stratos DC contains several template XML files used by the Nautilus application. However, these template XML files must be populated with valid data before they can be used. One of the daily tasks of a system admin working in the xFusionCorp industries is to apply string and file manipulation commands!
Replace all occurances of the string "Sample" to "Software" on the XML file /root/nautilus.xml located in the backup server.

```
ssh clint@stbkp01
sudo su -
cat /root/nautilus.xml |grep Sample | wc -l
cat /root/nautilus.xml |grep Sample
sed -i 's/Sample/Software/g' /root/nautilus.xml
cat /root/nautilus.xml |grep Software
cat /root/nautilus.xml |grep Software |wc -l
cat /root/nautilus.xml |grep Sample |wc -l
```