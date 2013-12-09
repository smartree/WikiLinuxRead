It's better to set up ssh to used key-based authentication rather than trying to figure out how to send text to the login process with something like expect.

Take a look at:

https://help.ubuntu.com/community/SSH/OpenSSH/Keys

So, basically, run ssh-keygen -t dsa on the machine that will run your script. When it asks you for a passphrase, hit ENTER to accept a blank. You will get two files. If you followed the default suggestions, the files will be ~/.ssh/id_dsa and ~/.ssh/id_dsa.pub. The first one is the private key. The second one is the public key.

Copy the public key to the second server using ssh-copy-id user@server2. This will add the public key to the authorized_keys file of the user on server2.

You should now be able to run ssh from the first machine and log in without a password.

For copying the files, scp or rsync are fine. It depends on what you're doing. rsync will use ssh by default, so will use the key-based authentication you just set up.


**Reference**
<http://serverfault.com/questions/318474/how-to-pass-password-to-scp-command-used-in-bash-script>