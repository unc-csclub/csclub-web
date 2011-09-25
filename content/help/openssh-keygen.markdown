---
title: Key-based authentication with OpenSSH
---

In the interests of security, the Computer Science Club Dominion Server only
accepts key-based authentication for logging into its SSH server.  This renders
brute-force password attacks ineffective, and reduces the potential for remote
access vulnerabilities.  Here’s a quick guide for OpenSSH users on how to
create your own key pair and use it to log in to the CSCDS.

<section markdown="1">
Creating your keys
==================

To generate a key pair, first run `ssh-keygen` at a shell prompt on your local
machine.  You’ll be prompted for a filename to use for the key pair (you can
enter nothing to accept the default of `~/.ssh/id_rsa`), then a passphrase:

    me@localhost:~$ ssh-keygen
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/me/.ssh/id_rsa): 
    Enter passphrase (empty for no passphrase): Enter same passphrase again: 

This passphrase is used to encrypt the private key on your local computer, so
it’s recommended that you pick a strong one so that your account is not open to
immediate compromise should the key files be lost.  After entering a filename
and passphrase, you’ll get something like the following output:

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

You’ll notice that two files have been created: a private key file with the
filename that you specified (here, `id_rsa`) and a corresponding public key
file (`id_rsa.pub`).  The private key is, as the name implies, only for
you&nbsp;— you’ll use the (decrypted) contents of this file, which the SSH
server checks against the public key on the server side, to log in.

Which means, of course, that you’ll need to get the public key on the server
first.  This is where you send an e-mail to the administrators with your SSH
username and the contents of `id_rsa.pub` (_not_ `id_rsa`, which is for your
eyes only and useless to the administrators anyway).
</section>

<section markdown="1">
Logging in for the first time
=============================

Once you’ve received word that your private key can be used to log in, you can
use the following command to specify your key file and log in to the CSCDS:

    ssh -i /home/me/.ssh/id_rsa me@csclub.cs.unc.edu

Of course, replace `me` with your username and the path after `-i` with the
actual path to the private key file if you specified a different one.  You
should be prompted for your passphrase, and if all goes well, you’ll get the
CSCDS welcome banner and a shell prompt.  Yay!
</section>

<section markdown="1">
Editing your SSH configuration file
===================================

Now, entering that entire command line every single time you want to log in
will get old _really_ quickly.  Fortunately, you can edit your `~/.ssh/config`
file and specify that you want to always send a certain key file and username
when you log in to the CSCDS.  Simply add the following lines to `config`,
creating it if it doesn’t exist:

    Host csclub.cs.unc.edu
    IdentityFile /home/me/.ssh/id_rsa
    User me

Now you can log in by simply entering `ssh csclub.cs.unc.edu`, and OpenSSH will
automatically pick up on your key file and username.
</section>
