## Linux
It contains all useful linux commands, more compilations could be found [here](#more-compilation)

###List open ports

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

### More Compilation
* [free][1]


[1]: ./free.md