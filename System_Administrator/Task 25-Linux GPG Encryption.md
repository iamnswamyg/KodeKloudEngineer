We have confidential data that needs to be transferred to a remote location, so we need to encrypt that data.We also need to decrypt data we received from a remote location in order to understand its content.
On storage server in Stratos Datacenter we have private and public keys stored /home/*_key.asc. Use those keys to perform the following actions.
Encrypt /home/encrypt_me.txt to /home/encrypted_me.asc.
Decrypt /home/decrypt_me.asc to /home/decrypted_me.txt. (Passphrase for decryption and encryption is kodekloud).

ssh natasha@ststor01
sudo su -
cd /home/
ll
gpg --import public_key.asc
gpg --import private_key.asc
gpg --list-keys
gpg --list-secret-keys
gpg --encrypt -r kodekloud@kodekloud.com --armor < encrypt_me.txt  -o encrypted_me.asc
gpg --decrypt decrypt_me.asc > decrypted_me.txt
 ll
 cat decrypted_me.txt
 cat decrypt_me.asc
 cat encrypt_me.txt
 cat encrypted_me.asc
