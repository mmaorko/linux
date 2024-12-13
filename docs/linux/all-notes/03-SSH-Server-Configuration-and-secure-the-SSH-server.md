## SSH Server Configuration and secure the SSH server
 ***OpenSSH Server*** : OpenSSH is a powerful collection of tools for remotely controlling networked computers and transferring data between them 
 
### SSH (Secure Shell or Secure Socket Shell) 
SSH is a network protocol that provides a secure connection between a client and server. All communication is encrypted, preventing theft of data transmitted over the network and other remote network attacks. Commonly used in UNIX-like systems, SSH servers authenticate users and ensure secure communication.

### SSH Architecture
SSH relies on the public-key cryptography to authenticate the remote system and allow it to authenticate the user trying to connect on it. SSH works on three hierarchical layers 

![Screenshot from 13-12-2024 2 10-01-24](https://i.ibb.co.com/Q8r6HS2/ssh-connection-init.png) 
<p align="center">Pic: SSH Connection Initialization </p>

#### Here is the detailed steps:

1. The client initiates a TCP connection to the SSH server on port 22 (default reserved port).
2. The server responds to the client’s connection and they establish a TCP handshake.
3. The server sends its identification string to the client with various informations (protocol version, etc).
4. The client sends its own identification informations to the server using the same format.
5. Once the identification strings have been exchanged, the server sends its public key to the client.
6. If the server is not in the “known_hosts” file of the client, it will prompt the user if they can trust it or not. If yes, the server will be added into the list.
   - If not, this question will prompted everytime
7. The client generates a random session key and encrypt it with the server’s public key.
8. The server decrypts the session key using its private key.
9. The connection between the client and the server is now secured by encrypting each data using the session key.
[References](https://blog.zedas.fr/posts/linux-explained-8-ssh/)

Then, the user is authenticated. This diagram displays the two authentication protocols : pub key then password.
![Screenshot from 13-12-2024 2 10-05-24](https://i.ibb.co.com/j5FLjj0/ssh-authentication.png) 

#### Authentication steps :

The client sends its authentication information to the server. Example here : its public key.
The server verifies is the public key is in the “authorized_keys” according to a deductive pattern.
If the client’s public key is not authorized, the server rejects it and notify the client.
The client tries to authenticate using the username and password.
The server validates the provided credentials.
The client and servers can now exchange data and commands in a secured encrypted way.

