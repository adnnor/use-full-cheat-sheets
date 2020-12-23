## GPG

Installation  
```bash
sudo apt install gnupg
```

#### Generating GPG Key Pair
The process will generate two kinds of keys, the Private Key and the Public Key

The Private key will allow you to encrypt your files, signed by this.

The Public key will allow you to verify the file encryption or signature, you can share this with the concerned person, so he or she might have access to relevant content.
```bash
gpg –gen-key
```

If you have been encountered with the error something like; `gpg: Sorry, no terminal at all requested - can't get input`, then make sure there is no extra configuration are made to `~/.gnupg/gpg.conf`, for example, might be you have configured your IDE for auto signing by putting `no-tty`, comment this line or one by one until the error disappears, and you have been taken to a screen to ask your real name. Please share your findings also!

It will take sometime and finally you will get your key pair generated and stored under `[HOME_DIR]/.gnupg`
