Initialize empty repository  
`git init`  

Set remote URL in your existing repository  
`git remote add [REMOTE_NAME] [REPO_URL]`  

Update the remote URL  
`git remote set-url [REMOTE_NAME] [REPO_URL]`  

Push set the upstream also so you don't need to mention remote branch  
`git push -u [REMOTE_NAME] [BRANCH_NAME]`  

Set upstream, e.g. map the local branch to remote branch  
`git branch --set-upstream-to [REMOTE_NAME]/[BRANCH_NAME]`  

Set the name for the current repo only  
`git config user.name "[NAME]"`  

Set the email for the current repo only  
`git config user.email "[EMAIL]"`  

Set name for all repositories globally  
`git config --global user.name "[NAME]"`

Set email for all repositories globally  
`git config --global user.email "[EMAIL]"`  

Update the author name and email of last commit  
`git commit --amend --author="[NAME] <[EMAIL]>"`

Disable file permission check, so the file with changed permission shouldn't be appeared under git staging  
`git config core.fileMode false`

Set the password for repositories globally, it will save the passwords under given location in readable format  
`git config --global credential.helper 'store --file ~/.git.cred'`

Set the password of current repository. It will save the password for the repository under given location in readable format  
`git config credential.helper 'store  --file ~/.git.cred'`

Unset the globally configured entry, after this it won't save the password until you have configured for any repository  
`git config --global --unset credential.helper`
