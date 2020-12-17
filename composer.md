## Composer
You can install the composer very easily, its pretty easy, after the successful installation you will be able to execute following commands  

Check composer version  
`composer --version`

Update composer to latest release  
`sudo composer self-update`  

Update composer to specific version  
`sudo composer self-update [VERSION]`  

Disables the automatic update of the dependencies. It is like removing entry from the `composer.json` without update  
`composer require [VENDOR]/[PACKAGE] [VERSION] --no-update`  

Remove specific package without affecting other installed packages. It will only remove the mentioned package  
`composer remove [VENDOR]/[PACKAGE]`

Ignore all platform requirements  
`composer update --ignore-platform-reqs`

Ignore specific platform requirement, in following example I am ignoring PHP platform requirement, so it will not check which PHP version you may have  
`composer install --ignore-platform-req=php`