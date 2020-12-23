## GPG

### Contents 
- [Installation](#installation)
- [Generate Key Pair](#generate-key-pair)
- [Github & GPG](#github--gpg)
- [List keys](#list-keys)
- [Import and export](#import-and-export)

### Installation

```bash
sudo apt install gnupg
```

### Generate Key Pair

The process will generate two kinds of keys, the Private Key and the Public Key

The Private key will allow you to encrypt your files, signed by this.

The Public key will allow you to verify the file encryption or signature, you can share this with the concerned person, so he or she might have access to relevant content.
```bash
gpg –gen-key
```

If you have been encountered with the error something like; `gpg: Sorry, no terminal at all requested - can't get input`, then make sure there is no extra configuration are made to `~/.gnupg/gpg.conf`, for example, might be you have configured your IDE for auto signing by putting `no-tty`, comment this line or one by one until the error disappears, and you have been taken to a screen to ask your real name. Please share your findings also!

It will take sometime and finally you will get your key pair generated and stored under `[HOME_DIR]/.gnupg`

### Github & GPG
> You can sign your work locally using GPG or S/MIME. GitHub will verify these signatures so other people will know that your commits come from a trusted source. GitHub will automatically sign commits you make using the GitHub web interface.
> [Source][1]

GitHub supports following GPG key algorithms, an unsupported algorithm may encounter an error.

* RSA
* ElGamal
* DSA
* ECDH
* ECDSA
* EdDSA

Create the GPG key with supported algorithm for GitHub
```bash
# If you are using GPG version > 2.1.17
gpg --full-generate-key
# For < 2.1.17
gpg --default-new-key-algo [Algo_With_Length] --gen-key
# example
gpg --gen-key --default-new-key-algo rsa2048 
```

Execute `gpg --list-secret-keys --keyid-format LONG` to list both public and private keys.
```bash
# example output

.../xxx.kbx
---------------------------
sec   rsa2047/34CAC1BA735E45G 
      03C35B85F64BE3B4504CA5235E1EBB012E497343F
uid                 [XXX]
ssb   rsa2047/7EB308882C33FA11
```
Now execute `gpg --armor --export 34CAC1BA735E45G > key.pub`, it will print the GPG key ID in ASCII armor format to key.pub, open the file and copy all the contents (CTRL+A).   

Head to GitHub > [Top Right Icon] > Settings > SSH and GPG Keys > New GPG Key > [Paste pub.key Contents] > Add GPG Key.

That's all, you have successfully added public GPG key to your GitHub account, now tell the [Git][2] client about this.

### List keys
[top](#contents)

```bash
# list public keys
gpg --list-keys

# list private keys
gpg --list-secret-keys

# list both public and private keys
gpg --list-secret-keys --keyid-format LONG
```

### Import and export
[top](#contents)

Once you have created the key pair, you can export in case you have changed your computer and doesn't want to create the key again.

**Export Public key**

```bash
gpg --export --armor [Email_Address]
# example
gpg --export --armor johndoe@example.com
# the key is exported to STDOUT so you can use following command to save the output to the file
gpg --export --armor johndoe@example.com > public
```

**Export Private key**
```bash
gpg --export-secret-keys --armor [Email_Address]
# example
gpg --export-secret-keys --armor johndoe@example.com
# or
gpg --export-secret-keys --armor johndoe@example.com > private.gpg
```

**Import key**
```bash
gpg --import [File_Path]
# example
gpg --import /path/to/public
```

[1]: https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/managing-commit-signature-verification
[2]: ../blob/master/git.md