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
SSH key with the passphrase will be prompted to enter the passphrase every time, avoid having to repeatedly do this, you can run an SSH agent. This small utility stores your private key after you have entered the passphrase for the first time.
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

### Change the default port
First of you have to check which service is running for SSH and what is the assigned port, to do;
```bash
grep 'ssh' /etc/services
```
Open the file;
```bash
sudo nano /etc/ssh/ssh_config
# or
sudo nano /etc/ssh/sshd_config
```
Search for `Port` by `CTRL+W` in `nano`, uncomment the line and change the value from 22 to any available port.

Restart the server;
```bash
sudo service ssh restart
# or
sudo service sshd restart
```
Remember that on latest linux, ssh service cannot be found, logout and login back will do the trick.

### Change passphrase of SSH key
```bash
ssh-keygen -p
```
You will be asked to enter the path of an existing key.

### Get the fingerprint of the key
```bash
ssh-keygen -l
```

### Copying your key to server




[1]: https://en.wikipedia.org/wiki/SSH_(Secure_Shell)