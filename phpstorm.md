
##### URN Highlighting
Magento code references all XSD schemas as Uniform Resource Names (URNs). If you are developing code and need to reference XSDs, this command configures your integrated developer environment (IDE) to recognize and highlight URNs. This makes development easier.

By default, an IDE like PhpStorm is not configured to recognize URNs and, as a result, they display in red text

https://devdocs.magento.com/guides/v2.4/config-guide/cli/config-cli-subcommands-urn.html

`bin/magento dev:urn-catalog:generate .idea/misc.xml` 



1 - install GPG tools : https://gpgtools.org/

2 - Create new key for your github email

3 - Add key to git on your local machine: git config --global user.signingkey YOURKEY

4 - configure git to sign all commits: git config --global commit.gpgsign true

5 - add to the bottom of ~/.gnupg/gpg.conf: (create the file if it not exists)

no-tty
use-agent
6 - Add key to you're github profile settings: gpg --armor --export YOURKEY