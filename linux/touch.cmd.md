## touch Command

This command create, change and modify timestamps of a file.

Don't mix with `cat`

**cat** command is used to create a file with content, whereas;  
**touch** command is used to create a file without content.

**Create empty file**

```bash
touch file.ext

# or to create multiple empty files
touch file1.ext file2.ext

# with custom date and time
touch -t YYMMDDHHMM file.ext
# e.g.
touch -t 200104171712 file.ext
# or
touch -t "17 Apr 2001" file.ext
```

**Change access time of a file**
```bash
touch -a file.ext
```

**Change modification time of a file**
```bash
touch -m file.ext
```

**Change access and modification time of a file**
```bash
touch -c-d file.ext
```

**Change the access and modification time of a file to given date and time**

```bash
touch -c -d "16 Aug 2001" ad.txt
touch -c -d 20010916 ad.txt
```

**Check file, if it is created or not**

The following command will check whether the file is created or not, if not then do not create, if it is created then it will change the access and modified time of an already created file.

```bash
touch -c file.ext
```

**Copy access and modify time from another file**

```bash
touch -r [source] [destination]
```