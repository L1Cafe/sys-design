# Describe SSH

SSH is a protocol for communicating securely over an unsecured network (such as the Internet). SSH stands for Secure Shell, as it was initially conceived to allow remote shell access to other systems.

The current version of SSH is SSH 2, and the version 1 is considered deprecated and insecure.

The most typical way to use SSH is to use either a username and password combination, or a username and private key file. SSH uses [asymmetric cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) for the initial authentication, and then proceeds to negotiate a [symmetric cryptography](https://en.wikipedia.org/wiki/Symmetric-key_algorithm) because symmetric cryptography is much more performant than asymmetric cryptography. Thus, this symmetric key will be used for sending and receiving the keystrokes and connection information. The latest versions of SSH also implement [rekeying](http://www.snailbook.com/faq/no-rekeying.auto.html), that allow server and client to re-negotiate a new symmetric key after a specified period of time, which works as a defense in case the symmetric key is ever leaked, guessed, or stolen, as the attacker will only have limited access to the connection, which will be lost after the rekeying.

SSH aims to replace telnet, as well as similar mechanisms, which all use insecure plain-text exchange of secrets. These protocols were designed at a time where the network would be trusted, but this is not the case anymore with the Internet.

SSH is often found as the only management protocol in networked Linux devices, and it is command-line only, unlike Windows' Remote Desktop Protocol which connects to a graphical session.

## Other SSH features

### Port tunnelling

You can forward ports from the client to the server, from the server to the client, or even use dynamic port forwarding to use with SOCKS-aware applications like web browsers. [More on port tunnelling](https://l1cafe.blog/2020/12/23/ssh-tunnelling.html)

### X11 forwarding

Due to the architecture of X11 (client-server), it is possible to forward X11 graphical sessions over SSH. While X11 is designed as a client-server protocol, X11 is unencrypted and is often highly restricted outside of `localhost`, therefore SSH will be able to add an encryption and authentication layer on top of any X11 graphical session. [More on X11 forwarding](https://unix.stackexchange.com/questions/12755/how-to-forward-x-over-ssh-to-run-graphics-applications-remotely)

### Remote commands

In addition to using SSH to obtain a shell onto a remote system, you can also remotely start commands using an SSH client. To run a command on a host, simply append it to the end of the command like so:

```
ssh username@myhost.com mycommand
```

Where `username` is the user to login with, `myhost.com` is the hostname of the SSH server, and `mycommand` is the command to run.

Note that this will not start a shell, and the SSH session will finish as soon as the command returns.
