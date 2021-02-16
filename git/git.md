## Git

Initialize empty repository  
```bash
git init
```  

Set remote URL in your existing repository  
```bash
git remote add [REMOTE_NAME] [REPO_URL]
```  

Update the remote URL  
```bash
git remote set-url [REMOTE_NAME] [REPO_URL]
```

Push set the upstream also so you don't need to mention remote branch  
```bash
git push -u [REMOTE_NAME] [BRANCH_NAME]  
```

Set upstream, e.g. map the local branch to remote branch  
```bash
git branch --set-upstream-to [REMOTE_NAME]/[BRANCH_NAME]  
```

Set the name for the current repo only  
```bash
git config user.name "[NAME]"  
```

Set the email for the current repo only  
```bash
git config user.email "[EMAIL]"
```  

Set name for all repositories globally  
```bash
git config --global user.name "[NAME]"
```

Set email for all repositories globally  
```bash
git config --global user.email "[EMAIL]"  
```

Update the author name and email of last commit  
```bash
git commit --amend --author="[NAME] <[EMAIL]>"
```

Disable file permission check, so the file with changed permission shouldn't be appeared under git staging  
```bash
git config core.fileMode false
```

Set the password for repositories globally, it will save the passwords under given location in readable format  
```bash
git config --global credential.helper 'store --file ~/.git.cred'
```

Set the password of current repository. It will save the password for the repository under given location in readable format  
```bash
git config credential.helper 'store  --file ~/.git.cred'
```

Unset the globally configured entry, after this it won't save the password until you have configured for any repository  
```bash
git config --global --unset credential.helper
```

Tell git about your gpg key
```bash
git config --global user.signingkey YOURKEY`  
git commit -S -m "Commit message"
```  
`-S` is used to sign the commit, onetime window will be appeared to ask your key password.  

Tell git that from now on each commits will be signed
```bash
git config --global commit.gpgsign true
git config commit.gpgsign true
```
`--global` will set the configuration as global otherwise it will be local to current repo where the command is executed.

**To make it working with PhpStorm**   
Open `~/.gnupg/gpg.conf`, and paste following two lines at the end of the file.
```bash
no-tty  
use-agent
```  
