
##### URN Highlighting
Magento code references all XSD schemas as Uniform Resource Names (URNs). If you are developing code and need to reference XSDs, this command configures your integrated developer environment (IDE) to recognize and highlight URNs. This makes development easier.

By default, an IDE like PhpStorm is not configured to recognize URNs and, as a result, they display in red text

https://devdocs.magento.com/guides/v2.4/config-guide/cli/config-cli-subcommands-urn.html

`bin/magento dev:urn-catalog:generate .idea/misc.xml` 

##### Sign commits
```bash
git config --global commit.gpgsign true
```

Create, if it not exists, or open ~/.gnupg/gpg.conf and add following lines at the end
```bash
no-tty
use-agent
```