## scp Command

> This command is used to copy file(s) between servers in secure way.

**Copy file to server**
```bash
# if remote server is configured for password
scp [file path] [user]@[remote host]:[remote path]
# e.g.
scp ~/Desktop/file.sql user@1.2.3.4:/var/www/
# if remote server is configured for identification file i.e. pem file.
scp -i [path to pem file] [file path] [user]@[remote host]:[remote path]
# e.g.
scp -i ~/Desktop/keys/server.pem ~/Desktop/file.sql user@1.2.3.4:/var/www/
```

Following options are available when you copy file to remote server.  

**V** - Used for verbosity i.e. provide the detail information of process.  
**p** - Copy modification and access times as well as modes from an original file.  
**C** - Compress file over network while transfer in progress, so the file could be transferred quickly. When the file is arrived to the remote server, it will return into the original size.  
**P** - Specify custom port.  
**r** - Copy recursively i.e. copy all files and directories from a directory recursively.  

**Download file from a server**
```bash
scp [user]@[remote host]:[remote path] [local path]
# or if pem file needs to be used
scp -i [path to pem file] [user]@[remote host]:[remote path] [local path]
# e.g.
scp username@1.2.3.4:/var/www/backup.tar ~/Downloads/backup.tar
# or
scp -i ~/Documents/server.pem username@1.2.3.4:/var/www/backup.tar ~/Downloads/backup.tar
```