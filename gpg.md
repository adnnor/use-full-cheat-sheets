## GPG
> GnuPG is a complete and free implementation of the OpenPGP standard as defined by RFC4880 (also known as PGP). GnuPG allows you to encrypt and sign your data and communications; it features a versatile key management system, along with access modules for all kinds of public key directories. GnuPG, also known as GPG, is a command line tool with features for easy integration with other applications. A wealth of frontend applications and libraries are available. GnuPG also provides support for S/MIME and Secure Shell (ssh).  
> Since its introduction in 1997, GnuPG is Free Software (meaning that it respects your freedom). It can be freely used, modified and distributed under the terms of the GNU General Public License.    
> The current version of GnuPG is 2.2.26. See the download page for other maintained versions.  
> Gpg4win is a Windows version of GnuPG featuring a context menu tool, a crypto manager, and an Outlook plugin to send and receive standard PGP/MIME mails. The current version of Gpg4win is 3.1.14. [Source][3]

So, GPG, or GNU Privacy Guard, is a public key cryptography implementation. This allows for the secure transmission of information between parties and can be used to verify that the origin of a message is genuine.

### Contents 
- [Installation](#installation)
- [Generate Key Pair](#generate-key-pair)
- [Github & GPG](#github--gpg)
- [List keys](#list-keys)
- [Delete keys](#delete-keys)
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

[top](#contents)

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

**Export**
```bash
# export public key
gpg --export --armor [Email_Address]

# example
gpg --export --armor johndoe@example.com

# the key is exported to STDOUT so you can use following command to save the output to the file
gpg --export --armor johndoe@example.com > public

# export private key
gpg --export-secret-keys --armor johndoe@example.com > private.gpg
```

**Import**
```bash
# import public key
gpg --import [File_Path]

# example
gpg --import /path/to/public

# import private key
gpg --allow-secret-key-import --import private.gpg
```

### Delete keys
[top](#contents)
```bash
# delete public key
gpg --delete-key [Email_Address]

# example
gpg --delete-key "johndoe@example.com"
```

If the public key is associated with the private key then you have to delete the private key first, otherwise you may encounter an error.

```bash
gpg: there is a secret key for public key "johndoe@example.com"!
gpg: use option "--delete-secret-keys" to delete it first.
```
```bash
# delete private key
gpg --delete-secret-key "johndoe@example.com"
```

[1]: https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/managing-commit-signature-verification
[2]: ./git.md
[3]: https://gnupg.org/
