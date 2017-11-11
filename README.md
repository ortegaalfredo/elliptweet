# elliptweet

Tweet using GnuPG ECC public key crypto

# Instructions
This is for debian/ubuntu:

## 1) If you don't have it, install GPG2:

```
$ sudo apt install gpgv2
```

## 2) Generate a ECC key:

```
$ gpg2 --expert --full-gen-key
gpg (GnuPG) 2.1.8; Copyright (C) 2015 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```

Then, we input 9 to select ECC primary key and ECC encryption subkey.

```
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
   (9) ECC and ECC
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
Your selection? 9
```
(see [here](https://www.gniibe.org/memo/software/gpg/keygen-25519.html))

## 3) Identify your key ID:

```
$ gpg2 --list-keys

pub   nistp256/CCF14DB4 2017-11-10 [SC]
uid         [ultimate] Alfredo Ortega <ortegaalfredo@gmail.com>

```

## 4) Generate application tokens:

This step is a bitch, it's explained [here](https://python-twitter.readthedocs.io/en/latest/getting_started.html).
You need four tokens:

consumer_key,consumer_secret,access_key and access_secret.

If neither the command line flags nor the enviroment variables are
present, the .tweetrc file, if it exists, can be used to set the
default consumer_key and consumer_secret.  The file should contain the
following three lines, replacing *consumer_key* with your consumer key, and
*consumer_secret* with your consumer secret:

A skeletal .tweetrc file:

```
[Tweet]
consumer_key: *consumer_key*
consumer_secret: *consumer_password*
access_key: *access_key*
access_secret: *access_password*
```


## 5) Finally, tweet:

```
$ ./elliptweet --keyid=CCF14DB4 --consumer-key=aaa --consumer-secret=bbb --access-key=ccc --access-secret=ddd --sign Check this out: https://git.io/vFVlQ
gpg: using "CCF14DB4" as default secret key for signing
Message len: 280

Message: 
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA25

Check this out: https://git.io/vFVlQ
-----BEGIN PGP SIGNATURE-----

iF4EARMIAAYFAloGVs4ACgkQZJQhd8zxTbRL3AD/ddpPzKvGdlOEC4O9y3BUtrA+
FK90TUhv/Rs0D2JUIU8BAP9HgE1najgmWlPG/d0cxRTeqSNdTbvyJrsA2ojgjC/L
=PbU6
-----END PGP SIGNATURE-----

Tweet? (Y/n):Y
```

That's it, enjoy. To decrypt/verify use gpg2 or the gpa gui.
Also you could use gpg2 directly and copy paste it, it's the same.

