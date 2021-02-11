## touch Command

This command create, change and modify timestamps of a file.

Don't mix with `cat`

**cat** command is used to create a file with content, whereas;  
**touch** command is used to create a file without content.

**Create empty file**

```bash
touch [file]

# or to create multiple empty files
touch [file] [file]

# with custom date and time
touch -t [date] [file]
# e.g.
touch -t 200104171712 file.txt
# or
touch -t "17 Apr 2001" file.txt
```

**Change access time of a file**
```bash
touch -a [file]
```

**Change modification time of a file**
```bash
touch -m [file]
```

**Change access and modification time of a file**
```bash
touch -c -d [file]
```

**Change the access and modification time of a file to given date and time**

```bash
touch -c -d [date] [file]
# e.g.
touch -c -d "16 Sep 2001" file.txt
# or
touch -c -d 20010916 file.txt
```

**Check file, if it is created or not**

The following command will check whether the file is created or not, if not then do not create, if it is created then it will change the access and modified time of an already created file.

```bash
touch -c [file]
```

**Copy access and modify time from another file**

```bash
touch -r [source] [destination]
```