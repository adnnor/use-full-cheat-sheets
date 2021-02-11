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
- [Revocation Certificate](#revocation-certificate)
- [Publish key](#publish-key)

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

### Revocation Certificate
[top](#contents)

What if 
* You have lost your private key?
* The key have been superseded?
* Your private key is compromised, like security breach?
* The key is no longer in use?
* You have forgotten the passphrase?

Now you want to revoke/disable that key, or you may say you want to invalidate your key pair, here comes the Revocation Certificate.
It is a revoked copy of your public key which you can publish to inform users that your public key should no longer be used.

Keep in mind that;
* You should generate this certificate when you make the keypair, not when you need it, because if you have lost your private there is no way you can create this certificate and won't be able to inform users.
* The revocation certificate must be generated ahead of time and kept in a secure location, best to keep it in separate location.
* Generating revocation certificate doesn't mean you are revoking the key you created.
* As you will be asked for the reason of revocation, so it is good to create a revocation certificate for each of likely scenarios and name them different.
* Before creating the revocation certificate, you will need to enter your GPG key’s passphrase to confirm your identity.
* The revocation certificate must be kept secure so that other users cannot revoke your key, best to print it.

```bash
gpg --output /path/johndoe_compromised.crt --gen-revoke johndoe@example.com
# or
gpg --output /path/johndoe_compromised.crt --generate-revocation johndoe@example.com
```

The revocation certificate will be written to the file specified by the --output flag.

To prevent unauthorized access immediately restrict the permissions on the generated certificate.
```bash
chmod 600 /path/johndoe_compromised.crt
```

### Publish key
[top](#contents)

It is time to publish your public key to the key server, it doesn't matter which key server you use, they synchronise their keys.

```bash
# publish key
gpg --keyserver [Keyserver_URL] --send-keys [Key_ID]

# search key
gpg --keyserver pool.sks-keyservers.net --search-keys [Public_Key]

# receive key
gpg --keyserver pool.sks-keyservers.net --receive-keys [Public_Key]
```

REMEMBER, OpenPGP key servers do not allow removal of the key with the fact that key servers are operated by hundreds of individuals so if you would ask the
individual operators to remove a key, they might block it on their own server, but others will still be hosting it. Revocation certificate is handy, you can create and publish it to key server.

```bash
# after creating revocation certificate, import the certificate
gpg --import /path/to/johndoe_compromised.crt
```

Now your key pair is invalidated, if you have uploaded/pushed/sent your keys to key servers then send the public key again so people may know about this.

```bash
gpg --keyserver [Keyserver_URL] --send-keys [Key_ID]
```

If you have sent the key to your friend, or concerned person, previously using any other medium then you have to export and send it again, so concerned party might know that your key is comprised or no longer in use.

Note: Other key server
> pgp.mit.edu
> keys.gnupg.net

### Wiki
sec => 'Secret key'   
ssb => 'Secret subkey'   
pub => 'public key'   
sub => 'public subkey'   

OpenPGP further supports subkeys, which are like the normal keys, except they're bound to a master key pair. A subkey can be used for signing or for encryption. The really useful part of subkeys is that they can be revoked independently of the master keys, and also stored separately from them.

In other words, subkeys are like a separate key pair, but automatically associated with your main key pair.

...

You should keep your private master key very, very safe

...

Subkeys make this easier: you already have an automatically created encryption subkey and you create another subkey for signing, and you keep those on your main computer. You publish the subkeys on the normal keyservers, and everyone else will use them instead of the master keys for encrypting messages or verifying your message signatures.

...

You will need to use the master keys only in exceptional circumstances, namely when you want to modify your own or someone else's key.

PUBKEY_USAGE_SIG      S
PUBKEY_USAGE_CERT     C
PUBKEY_USAGE_ENC      E
PUBKEY_USAGE_AUTH     A

'--list-options parameters'

show-usage

      Show usage information for keys and subkeys in the standard
      key listing.  This is a list of letters indicating the allowed
      usage for a key ('E'=encryption, 'S'=signing,
      'C'=certification, 'A'=authentication).  Defaults to no.

So, doing gpg -k --list-options show-usage 1A3ABKEY will show you something like this:

pub   rsa4096/1A3ABKEY 2015-01-25 [SC]
uid         [ultimate] Some Key
sub   rsa4096/4B907KEY 2015-09-19 [S]
sub   rsa4096/F9A41KET 2015-09-19 [E]

The OpenPGP (v4) key ID is an identifier calculated from the public key and key creation timestamp. From those, a hashsum is calculated. The hex-encoded version is called the fingerprint of the key. The last (lower order) 16 characters are called the long key ID, if you only take the last eight characters, it's the short key ID. An example for my own public key:

fingerprint: 0D69 E11F 12BD BA07 7B37  26AB 4E1F 799A A4FF 2279
long id:                                    4E1F 799A A4FF 2279
short id:                                             A4FF 2279

The (long) key id is represented by the lowest 64 bits, and is used as the full fingerprint is an unhandy and long value. Even more often, the short key id formed by the lowest-order 32 bits is used. These short key IDs are often considered to have a too high chance of collisions and usage of at least the long ID, if not even full fingerprint is recommended.

The Key ID of the Primary public key (‘366150CE’ in this case) is used to refer to some of its own subkeys, such as the associated private signing key, as well as the encryption subkey.

The fingerprint/key id is a hash of the entire key packet, and only the key packet. It is invalidated (changed) if any information in the key packet is changed, but is unaffected by any changes in any other packets.

n RFC2822 format (“David Steele <dsteele@gmail.com>”)

Flag	gpg character	Description
0x01	“C”	Key Certification
0x02	“S”	Sign Data
0x04	“E”	Encrypt Communications
0x08	“E”	Encrypt Storage
0x10	 	Split key
0x20	“A”	Authentication
0x80	 	Held by more than one person



[1]: https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/managing-commit-signature-verification
[2]: ../git.md
[3]: https://gnupg.org/
