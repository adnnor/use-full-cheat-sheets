## Magento Cloud

##### Access the Web Panel
https://accounts.magento.cloud/user
https://www.magentocommerce.com/products/login

### Install magento-cloud CLI
```bash
curl -sS https://accounts.magento.cloud/cli/installer | php
source $HOME/.bashrc
```
You will get similar response

```bash
Magento Cloud CLI installer

Environment check
[*] The "json" PHP extension is installed.
[*] The "phar" PHP extension is installed.
[*] Git is installed.
[*] The "openssl" PHP extension is installed.
[*] The "pcre" PHP extension is installed.
[*] One or both of the "mbstring" or "iconv" PHP extensions is installed.
[*] The "curl" PHP extension is installed.
[*] The "pcntl" and "posix" extensions are installed.
[*] The "allow_url_fopen" setting is on.
[*] The "apc.enable_cli" setting is off.

Download
Finding the latest version... done
Downloading version 1.37.0... done
Checking file integrity... done
Checking that the file is a valid Phar... done
[...]
```

#### Login
```bash
# when the installation is finished
# to check available commands
magento-cloud list

# login to Magento Cloud
magento-cloud login
```

### Common Commands
Altough you can list all commands using `magento-cloud list` command, I am listing some of the common commands and their usages.
##### List projects
```bash
magento-cloud project:list
# or
magento-cloud projects
```

##### SSH keys
```bash
# list keys
magento-cloud ssh-key:list 
#or
magento-cloud ssh-keys

# add key
magento-cloud ssh-key:add ~/.ssh/id_rsa.pub

# delete key
magento-cloud ssh-key:delete [id]
```

##### Variables
```bash
# list
magento-cloud variable:list
# or
magento-cloud variables

# get value or variable
magento-cloud variable:get [name]

# create variable
magento-cloud variable:create

# update variable
magento-cloud variable:update [name]

# delete variable
magento-cloud variable:delete [name]
```

git remote rm magento
git remote add origin [new git url]

magento-cloud build

== git checkout -b
magento-cloud environment:branch <name> <parent-branch>

== git checkout
magento-cloud environment:checkout <environment-ID>

db:dump Create a local dump of the remote database
db:size Estimate the disk usage of a database
db:sql (sql) Run SQL on the remote database