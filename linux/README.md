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

### More Compilation
* [free][1]
* [gpg][2]
* [touch][3]
* [find][4]


[1]: ./free.md
[2]: ./gpg.md
[3]: ./touch.cmd.md
[4]: ./find.md