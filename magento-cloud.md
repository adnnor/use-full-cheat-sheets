## Magento Cloud

### Contents
- [Access the Web Panel](#access-the-web-panel)
- [Installation](#installation)
- [Common Commands](#common-commands)
- [Setup Project](#setup-project)
- [Database](#database)

### Access the Web Panel
https://accounts.magento.cloud/user   
https://www.magentocommerce.com/products/login

### Installation
```bash
curl -sS https://accounts.magento.cloud/cli/installer | php
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
When  the installation is finished
```bash
source ~/.bashrc # (make sure your shell does this by default)
```
When the installation is finished, it is time to login to Magento Cloud
```bash
magento-cloud login
```

### Common Commands
[top](#contents)   

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

### Setup Project
[top](#contents)   

To setup your cloud project on your localhost, login to Magento Cloud (magento-cloud login) 

```bash
# to list available projects
magento-cloud projects
# or
magento-cloud project:list

# example output
Your projects are: 
+---------------+-------------+------------------------------------------------+
| ID            | Title       | URL                                            |
+---------------+-------------+------------------------------------------------+
| xxx           | xxx         | xxx                                            |
+---------------+-------------+------------------------------------------------+

Get a project by running: magento-cloud get [id]
List a project's environments by running: magento-cloud environments -p [id]
```

Now clone your project, 

```bash
magento-cloud project:get <project-ID>
# or
magento-cloud get [id]
```

You can list available environments
```bash
magento-cloud environment:list
# or 
magento-cloud environments
```
> The magento-cloud environment:list command displays environment hierarchies, whereas the git branch command does not. [Source][1]

Once the clone is completed, install all dependencies.

```bash
composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
```

### Database
[top](#contents)

Create the local dump of the remote database
```bash
db:dump
```

Estimate the disk usage of a database
```bash
db:size
```

Run SQL queries on the remote database
```bash
db:sql
```

[1]: https://devdocs.magento.com/cloud/before/before-setup-env-2_clone.html