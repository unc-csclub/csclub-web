---
title: Key-based authentication with OpenSSH
---

In the interests of security, the Computer Science Club server requires that users who log in through SSH use key-based authentication.
This renders brute-force password attacks ineffective, and reduces the potential for remote access vulnerabilities.
Here's a quick guide for OpenSSH users on how to create your own key pair and use it to log in to the CSC server.


<section markdown="1">
Creating your keys
==================

To generate a key pair, first run `ssh-keygen` at a shell prompt on your local machine.
You'll be prompted for a filename to use for the key pair (you can enter nothing to accept the default of `~/.ssh/id_rsa`), then a passphrase:

    me@localhost:~$ ssh-keygen
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/me/.ssh/id_rsa):
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:

This passphrase is used to encrypt the private key on your local computer.
You can use a blank passphrase for convenience, but it's recommended that you pick a strong one so that your account is not open to immediate compromise should the key files be lost.
After entering a filename and passphrase, you'll get something like the following output:

    Your identification has been saved in /home/me/.ssh/id_rsa.
    Your public key has been saved in /home/me/.ssh/id_rsa.pub.
    The key fingerprint is:
    12:34:56:78:9a:bc:de:f0:12:34:56:78:9a:bc:de me@localhost
    The key's randomart image is:
    +--[ RSA 2048]----+
    | ..o.            |
    | .o..o           |
    |o..oo .          |
    |+o.. o           |
    |E . . o S        |
    |=o + . .         |
    |+.o .            |
    | ..o             |
    | .. .            |
    +-----------------+

You'll notice that two files have been created: a private key file with the filename that you specified (here, `id_rsa`) and a corresponding public key file (`id_rsa.pub`).
The private key is, as the name implies, only for you --- you'll use the (decrypted) contents of this file, which the SSH server checks against the public key on the server side, to log in.
Of course, this means that you'll need to get the public key on the server first.
To do that, you'll need to contact the administrators with your SSH username and the contents of the public key file.
(Make sure that you aren't accidentally sending your private key; the administrators won't be able to do much with it, anyway.)
</section>


<section markdown="1">
Logging in for the first time
=============================

Once you've received word that your public key has been added to the server, you can use the following command to log in:

    ssh -i ~/.ssh/id_rsa me@csclub.cs.unc.edu

Replace `me` with your username, and the path after `-i` with the actual path to the private key file if you specified a different one.
You'll be prompted for your passphrase if you specified one when creating your private key.
Should you successfully log in, you'll be presented with a greeting message and a shell prompt.
</section>


<section markdown="1">
Editing your OpenSSH configuration file
=======================================

For convenience, you can specify most of the options given on the command line above to your `~/.ssh/config` file and save yourself some typing.
Add the following lines to `config`, creating it if it doesn't exist:

    Host csclub.cs.unc.edu
    IdentityFile ~/.ssh/id_rsa
    User me

This instructs your client to automatically send the private key at `~/.ssh/id_rsa` and the username `me` to the server.
You may now log in by simply entering `ssh csclub.cs.unc.edu`, and OpenSSH will
handle the rest.
</section>
