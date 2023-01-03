There is some data on Nautilus App Server 2 in Stratos DC. Data needs to be altered in several of the files. On Nautilus App Server 2, alter the /home/BSD.txt file as per details given below:

a. Delete all lines containing word "following" and save results in /home/BSD_DELETE.txt file. (Please be aware of case sensitivity)
b. Replace all occurrence of word "and" to "them" and save results in /home/BSD_REPLACE.txt file.

Note: Let's say you are asked to replace word to with from. In that case, make sure not to alter any words containing this string; for example upto, contribu to r etc.

ssh steve@172.16.238.11
sudo su -
cd /home/
cp BSD.txt BSD_DELETE.txt
cp BSD.txt BSD_REPLACE.txt

#Delete
fgrep following BSD_DELETE.txt
sed -i '/following/d' BSD_DELETE.txt
fgrep following BSD_DELETE.txt

#Replace
fgrep and BSD_REPLACE.txt
sed -i -r 's/and/them/g' BSD_REPLACE.txt
fgrep them BSD_REPLACE.txt