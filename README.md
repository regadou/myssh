This is myssh, a wrapper script for using ssh and scp with a private key file.

To install, just copy or symlink the myssh file to a folder that is on your path. Make sure it has the executable bit set. You will also need a .myssh file in your home folder that you must populate according to the instructions below.

The .myssh file in your home folder should have one entry per line where each entry contains 3 fields separated by a colon (:). The 3 fields should be the service name, user@host and private key file for each remote ssh service you want to access. For instane, if you want to access a service named "my-server" on host example.com with username "me" and private key file at /home/local-user/.ssh/my-server.pem then you should have an entry in .myssh like the following:

   :my-server:me@example.com:/home/local-user/.ssh/my-server.pem
   
You will the be able to login to this host with the following command:

   myssh my-server
   
If you just want to list the content of the /var/www folder on the remote host without an interactive, you would then issue the following command:

   myssh my-server ls -al /var/www
   
Beware of the wildard usage. To prevent a wildcard (*) from being expanded on the local host but only on the remote host, surround it with single quotes:

   myssh my-server ls -al '/var/www/*.html'

To copy files between local and remote hosts, you can do the following:

   myssh my-server copy /var/www/index.html somedir/index.html
   
Copying files can be done in both directions. So in order to know which file is local and which one is remote, myssh will consider the file starting with / as being the remote one. If none or both files start with / then myssh will give you an error message. Because of this behavior, the local file is always going to be relative to the current directory. So make sure you cd into the local directory of your choice before issuing any myssh copy command.

Also, please note that the copy command is explicitely named "copy" to distinguish it from "cp" which would execute a file copy from source to target on the remote host only.

