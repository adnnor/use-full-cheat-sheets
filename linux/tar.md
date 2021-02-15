## tar Command

> "tar" stands for "**t**ape **ar**chive". The tar command used to rip a collection of files and directories into highly compressed archive file a commonly called tarball or tar, gzip and bzip in Linux. The tar is most widely used command to create compressed archive files and that can be moved easily from one disk to another disk or machine to machine.

**Create archives**
```bash
# tar
tar -cf [tarball archive name] [path of file or directory]
# tar.gz
tar -zcf [tar.gz archive name] [path of file or directory]
# tar.bz2
tar -jcf [tar.bz2 archieve name] [path of file or directory]
# e.g.
tar -cf dump.tar /home/ad/Desktop/dump.sql
# or to add multiple files or directories
tar -cf dump.tar "/home/ad/Desktop/dump.sql" "/home/ad/Desktop/dump2.sql"
```

**Add a file or directory to existing tarball**  
Following command will help you to add a file or directory to existing tar archive, remember, you cannot append a compressed archive such as bz2 or bz.
```bash
tar -rf [path.tar] [path of file or directory to append]
# e.g.
tar -rf backups.tar /home/ad/dumps
```

**List the contents of an archive**
```bash
tar -tf [archive path]
```

**Untar/uncompress archive**
```bash
# in current directory
tar -xf [archive path]
# in specified directory
tar -xf [archive path] -C [path to extract]
```

**Untar/uncompress a single or multiple files**
```bash
# for tarball
tar -xf [archive path] "file1.txt" "file2.sql"
# or use wildcard to extract matching files
tar -xf [archive path] --wildcards "*.sql"
# for gz
tar -zxf [archive path] "file1.txt" "file2.sql"
tar -zxf [archive path] --wildcards "*.sql"
# for bz2
tar -jxf [archive path] "file1.txt" "file2.sql"
tar -jxf [archive path] --wildcards "*.sql"
```

**Verify tarball archives**
Note: It doesn't work with bz2 or gz archive 
```bash
tar -Wtf [path.tar]
```

### List of available commands
**c** – create an archive.  
**j** – create bzip2 archive.  
**z** – create gzip archive.  
**f** – filename of archive.  
**r** – append or update files or directories to existing archive file.  
**v** – verbosity, show the progress of archive file.  
**t** – list contents of archive.  
**wildcards** – Specify patterns in unix tar command.  
**W** – Verify an archive.  
**x** – extract an archive.  
