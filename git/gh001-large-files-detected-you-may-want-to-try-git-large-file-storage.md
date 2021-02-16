## Fixing the "GH001: Large files detected. You may want to try Git Large File Storage."

When you are trying to push your changes with having bigger files somewhere in the repo, you might get following error.

```bash
[...]
remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
remote: error: Trace: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
remote: error: See http://git.io/iEPt8g for more information.
remote: error: File [path] is [size]; this exceeds GitHubs file size limit of 100.00 MB
remote: error: File [path] is [size]; this exceeds GitHubs file size limit of 100.00 MB
[...]
```

GitHub only allows for 100 MB file as mentioned. If you have already committed, then removing file(s) will not help because it is tracked inside the previous commits, so you can fix this issue with following command.

```bash
git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch [path/to/big/file]'
```

Push your changes again and the action will be successfully completed.