## Linux
It contains all useful linux commands, more compilations could be found [here](#more-compilation)

### Contents

- [List open ports](#list-open-ports)
- [Create a symbolic (shortcut) link](#create-a-symbolic-shortcut-link)
- [Switch the PHP version of terminal](#switch-the-php-version-of-terminal)
- [Add user to group](#add-user-to-group)
- [Delete user](#delete-user)
- [List groups, users and active users](#list-groups-users-and-active-users)

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
### Add user to group   

If the user is already existed then you can use following command to add user to a group, otherwise, you have to create the user first by executing a command `sudo adduser [user]`, by default, the home directory is named as username, you can change this by `sudo adduser --home /home/[custom name] ad`.

```bash
sudo usermod -aG [user] [group]
# or
sudo adduser [user] [group]
```

Users are stored under `/etc/passwd`, passwords are under `/etc/shadow` and groups are stored under `/etc/group`.

Note: By default only the first user has the ability to use `sudo`, every other user will face an error of `[user] is not in the sudoers file` (or similar). 
To get rid of this error or if you would like to give other user a capability to execute command with `sudo`, then you can execute aforementioned command to add user to sudoers, e.g. `sudo adduser [user] sudo`.

You can change the password of a user by executing a command `passwd [user]`

### Delete user

```bash
sudo userdel [user]
# or to delete user's home directory also
sudo userdel -r [user]
# or
sudo userdel --remove-home [user]
```

You can remove user from the group by executing `sudo deluser [user] [group]`

### List groups, users and active users

As users are saved under `/etc/passwd`, each line describe distinct user and its information. If you would like to list only the usernames then use `cut` command with following syntax;

```bash
cut -d : -f 1 /etc/passwd
# or for groups
cut -d : -f 1 /etc/group
```

How above command is working? The `-d` option is used for a delimiter, which is `:`, then the `-f` option is used to specify field number i.e. 1st.

So it is, cut/break the contents of given file with provided delimiter and return the first column or field.

**Sample output for `/etc/group`**

```bash
root:x:x:
daemon:x:x:
bin:x:x:
```

**Sample output for `/etc/passwd`**

```bash
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
```

**Sample output for `/etc/shadow`**

```bash
root:!:xxxxx:0:xxxx:x:::
daemon:*:xxxxx:0:xxxx:x:::
bin:*:xxxx:0:xxxx:x:::
```

`w` or `who` command is used to check all active/logged users on the machine.

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