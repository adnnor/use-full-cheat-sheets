## mkdir Command

> This command is used to create directories.

### Create a directory
```bash
mkdir [name and path]
# e.g.
mkdir /var/www/directory
# or create multiple directories in single path
mkdir /var/www/{one,two,three}

# with verbosity
mkdir -v /var/www/directory
# or
mkdir --verbose /var/www/directory
# or without path it will create the new directory under current path
mkdir --verbose directory
```

### Create directory (recursive)
Create parent directories as necessary, if the directories exist, no error is specified.
```bash
mkdir -p hello/world/foo/bar
# or 
mkdir -p /var/www/hello/world/foo/bar
# or
mkdir --parents foo/bar
```

### Create a directory (with custom permissions)
Set the permissions for the created directory, it will use syntax as `chmod`.
```bash
mkdir -m 600 directory
```

