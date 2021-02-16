## SSH

> SSH or Secure Shell is a cryptographic network protocol for operating network services securely over an unsecured network. Typical applications include remote command-line, login, and remote command execution, but any network service can be secured with SSH. [Source][1]

### Check for existing SSH keys

```bash
ls -al ~/.ssh
```

### Create new SSH key pair

```bash
ssh-keygen -t ed25519 -C "[email address]"
# If you are using a legacy system that doesn't support the Ed25519 algorithm
ssh-keygen -t rsa -b 4096 -C "[email address]"
```

### Add key to your SSH agent

```bash
# start the ssh-agent
eval "$(ssh-agent -s)"
# now add the key to ssh-agent
ssh-add ~/.ssh/[key name]
```

Sample output

```bash
Enter passphrase for /home/user/.ssh/[key name]: 
Identity added: /home/user/.ssh/[key name] (john@example.com)
```

[1]: https://en.wikipedia.org/wiki/SSH_(Secure_Shell)