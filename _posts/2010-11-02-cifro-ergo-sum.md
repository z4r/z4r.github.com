---
layout: post
category : utility
tags : [crypto, gpg]
---
{% include JB/setup %}

### Generate a key-pair
    $ gpg --gen-key

### Upload the key
    $ gpg --send-keys --keyserver pgp.mit.edu $KEYID

### Revoke a key
    $ gpg --gen-revoke $KEYID

Save the certificate-block in `$FILE` .
Import the revocation certificate:

    $ gpg --import $FILE
Check the key is correctly revoked:

    $ gpg --list-sigs $KEYID
Should say _revoked_ in the first line and _rev_ in the second one.

### Upload the revoked key
    $ gpg --send-keys --keyserver pgp.mit.edu $KEYID

### List all keys
    $ gpg --list-keys

### List a specific key
    $ gpg --list-keys $NAME
or:

    $ gpg --list-keys $KEYID

### Export the public key
    $ gpg --export --armor $KEYID > pubkey.txt

### Export the private key
    $ gpg --export-secret-keys --armor $KEYID > pubkey.txt

### Import a public or private key
    $ gpg --import $FILE
    $ gpg --recv-keys --keyserver pgp.mit.edu $KEYID

### Interactively edit a key
    $ gpg --edit-key $KEYID

### Encrypt symmetric (very strong):
    $ gpg --cipher-algo RIJNDAEL256 -o $CRYPT-FILE -c $PLAIN-FILE

### Decrypt symmetric:
    $ gpg --cipher-algo RIJNDAEL256 -o $PLAIN-FILE --decrypt $CRYPT-FILE

