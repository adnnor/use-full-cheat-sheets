## Linux
It contains all useful linux commands, more compilations could be found [here](#more-compilation)

### List open ports

Run any one of the following command on Linux to see open ports  
```bash
sudo lsof -i -P -n | grep LISTEN
sudo netstat -tulpn | grep LISTEN
# to see specific port e.g. 22
sudo lsof -i:22
sudo nmap -sTU -O IP-address-Here
# on versions of Linux 
ss -tulw
```

### Create a symbolic (shortcut) link

A symbolic link, symlink or soft link, is a special type of file that points to another file or directory.

Without using `-s` or `--symbolic` option, `ln` will create hard link.
```bash
ln -s [source] [destination]
# or
ln --symbolic [source] [destination]
# overwrite the destination path of the symlink
ln -sf [source] [destination]
# or 
ln --symbolic --force [source] [destination]
```

### Switch the PHP version of terminal
```bash
# interactive
sudo update-alternatives --config php
sudo update-alternatives --config phar
sudo update-alternatives --config phar.phar

# manual
sudo update-alternatives --set php /usr/bin/php7.4
sudo update-alternatives --set phar /usr/bin/phar7.4
sudo update-alternatives --set phar.phar /usr/bin/phar.phar7.4
```

### More Compilation
* [free][1] - Provides information about memory.
* [gpg][2] - Allows you to encrypt and sign your data and communications.
* [touch][3] - Create, change and modify timestamps of a file.
* [find][4] - Search and locate the list of files and directories.
* [tar][5] - Rip a collection of files and directories into highly compressed archives.
* [scp][6] - Copy file(s) between servers in secure way.


[1]: ./free.md
[2]: ./gpg.md
[3]: ./touch.cmd.md
[4]: ./find.md
[5]: ./tar.md
[6]: ./scp.md