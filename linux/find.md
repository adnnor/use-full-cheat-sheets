## find Command

> This command is used to search and locate the list of files and directories based on conditions you specify for files that match the arguments.

**Find [file] in [path]**
```bash
find [path] -name [file]
# or use iname for case insensitive match
find [path] -iname [file]
```

**Fine all files in [path] with matching criteria**
```bash
find [path] -type -f -name "*.php"
# or to find hidden files
find [path] -type -f -name ".*"
```

**Fine all directories in [path] with matching criteria**
```bash
find [path] -type -d -name "Directory"
```

**Find all files in [path] have given [permission]**
```bash
find [path] -type -f -perm [permission]
# or don't have given [permission]
find [path] -type -f ! -perm [permission]
```

**Find files in [path] and execute chmod command**
```bash
find [path] -type -f -exec chmod 644 {} \; 
# or find directories
find [path] -type -d -exec chmod 755 {} \; 
```

**Fine audio files in [path] and remove all of them**
```bash
find [path] -type f -name "*.mp3" -exec rm -f {} \;
```

**Find empty files in [path]**
```bash
find [path] -type -f -empty
# or for directories
find [path] -type -d -empty
```

**Find all files in [path] associated with the linux [user]**
```bash
find [path] -user [user]
# or linux [group]
find [path] -group [group]
```

**Find all files larger than 50M**
```bash
find [path] -size +5M
# or less than 5M
find [path] -size -5M
# or exactly 5M
find [path] -size 5M
# or greater than 5 and less than 10M
find [path] -size +5M -size -10M
```

**find all files in [path] which is changed in last [minutes] minutes**
```bash
find [path] -ctime [minutes]
# or accessed
find [path] -atime [minutes]
# or modified
find [path] -mtime [minutes]
```