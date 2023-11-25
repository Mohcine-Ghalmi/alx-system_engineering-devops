# CREATE A server
<br>
<img src="image-3.png" style="display: block;margin: auto;"><br>

## What is a (physical) server:
<br>
<img src="image-1.png" style="display: block; margin: auto;">
<br>

>A server is a computer hardware or software that provides services to other programs or devices, known as clients. It follows a client-server model where servers can perform tasks like sharing data or resources among multiple clients or performing computations for a client. A server can serve multiple clients, and a client can use multiple servers. The client process can run on the same device or connect to a server on a different device over a network. Examples of servers include <b>database servers, file servers, mail servers, print servers, web servers, game servers, and application servers</b>.

## SSH essentials
<br>
<img src="image.png" style="display: block; margin: auto;">
<br>
>SSH is a secure protocol used to connect to Linux servers remotely. It allows you to interact with the server by sending commands from your local terminal, which are then executed on the remote server.

### SSH Overview
> The most common way to connect to a remote Linux server is through SSH. SSH stands for <b>Secure Shell</b> and allows you to securely execute commands, make changes, and configure services on the remote server. When you connect via SSH, you use an account that exists on the remote server.

### How SSH Works

>When you connect to a server using SSH, you will be able to interact with it through a text-based interface called a shell session. This allows you to send commands from your local terminal to the server, where they are executed. The SSH connection ensures that the commands are securely transmitted through an encrypted tunnel.

>An SSH connection works like a conversation between two parties: the client and the server. The client is the user's computer, and the server is the remote machine. To establish an SSH connection, the remote machine needs to have a special software called an SSH daemon. This software listens for connection requests, checks the credentials provided by the client, and creates a secure environment for the client to interact with.

>To connect to a remote host using SSH, your computer needs to have an SSH client. This client software understands how to communicate using the SSH protocol and requires information about the remote host, username, and authentication credentials. The client can also specify the type of connection they want to establish.

### How SSH Authenticates Users

> Clients can authenticate using either passwords (less secure) or SSH keys (more secure).

> Password logins are easy to understand but can be targeted by automated bots and malicious users. To enhance security, it is recommended to use SSH key-based authentication.

> SSH keys consist of a public and a private key. The public key can be freely shared, while the private key must be kept secure.

> To authenticate using SSH keys, the user needs to have a key pair on their local computer. The public key must be copied to the `~/.ssh/authorized_keys` file on the remote server. This file contains a list of authorized public keys.

> When a client connects to the server and wants to use SSH key authentication, it informs the server and specifies which public key to use. The server checks its `authorized_keys` file for the public key, generates a random string, and encrypts it using the public key. The encrypted message is sent to the client.

> The client decrypts the message using the private key, combines the revealed random string with a session ID, generates an MD5 hash, and sends it back to the server. The server compares the MD5 hash with the original values to verify the client's private key.

### Generating an SSH Key Pair

>To authenticate with a remote server without a password, you need to generate a new SSH public and private key pair on your local computer. It is recommended to always use SSH keys for authentication, unless there is a specific reason not to.

>There are different cryptographic algorithms that can be used to generate SSH keys, such as RSA, DSA, and ECDSA. RSA keys are commonly used and are the default key type.

To generate an RSA key pair on your local computer, you can use the following command:<br>
<pre>
    <code>
        $ ssh-keygen
    </code>
</pre>
<pre>
    <code>
        Generating public/private rsa key pair. <br>
        Enter file in which to save the key (/home/demo/.ssh/id_rsa):
    </code>
</pre>

When generating an RSA key pair on your local computer, you have the option to choose the location to store your RSA private key. By default, the keys are stored in the `.ssh` hidden directory in your user's home directory. If you press ENTER without specifying a different location, the keys will be stored in the default location. Storing the keys in the default location allows your SSH client to find them automatically.

<pre>
    <code>
        Enter passphrase (empty for no passphrase):
        Enter same passphrase again:
    </code>
</pre>

>When generating an RSA key pair on your local computer, you have the option to set a passphrase to secure your private key. By default, you will be prompted to enter the passphrase every time you use the private key, adding an extra layer of security. If you prefer not to set a passphrase, you can simply press ENTER. However, keep in mind that this will allow anyone who gains access to your private key to log in to your servers.

>If you choose to set a passphrase, it will not be displayed as you type for security reasons.

<pre>
    <code>
        Output
        Your identification has been saved in /root/.ssh/id_rsa.
        Your public key has been saved in /root/.ssh/id_rsa.pub.
        The key fingerprint is:
        8c:e9:7c:fa:bf:c4:e5:9c:c9:b8:60:1f:fe:1c:d3:8a root@here
        The key's randomart image is:
        +--[ RSA 2048]----+
        |                 |
        |                 |
        |                 |
        |       +         |
        |      o S   .    |
        |     o   . * +   |
        |      o + = O .  |
        |       + = = +   |
        |      ....Eo+    |
        +-----------------+
    </code>
</pre>

>This procedure has generated an RSA SSH key pair, located in the .ssh hidden directory within your user’s home directory. These files are:

>~/.ssh/id_rsa: The private key. DO NOT SHARE THIS FILE! <br>
~/.ssh/id_rsa.pub: The associated public key. This can be shared freely without consequence.
