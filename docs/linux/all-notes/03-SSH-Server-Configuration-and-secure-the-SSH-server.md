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

Then, the user is authenticated. This diagram displays the two authentication protocols : pub key then password.
![Screenshot from 13-12-2024 2 10-05-24](https://i.ibb.co.com/j5FLjj0/ssh-authentication.png) 

#### Authentication steps :

1. The client sends its authentication information to the server. Example here : its public key.
2. The server verifies is the public key is in the “authorized_keys” according to a deductive pattern.
4. If the client’s public key is not authorized, the server rejects it and notify the client.
5. The client tries to authenticate using the username and password.
6. The server validates the provided credentials.
7. The client and servers can now exchange data and commands in a secured encrypted way.

## Steps 1:  Install SSH on Ubuntu
OpenSSH is not pre-installed on the system, so let's install it manually. To do this, type in the terminal update packages to the latest versions and install `openssh-server` package.
```bash
sudo apt update
sudo apt install openssh-server
```

## Steps 2: Start and Enable SSH Service
Verify that the service is running successfully, and enable service.
```bash
sudo systemctl status ssh
sudo systemctl enable --now ssh
```

## Steps 3: Configure custom SSH port
The default SSH port is 22 and most of the attack scripts check are written around this port only. Changing the default SSH port should add an additional security layer because the number of attacks (coming to port 22) may reduce.\

**Before making any changes to configuration files, it's always a good practice to back them up.** 

`sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config_back`

`sudo vim /etc/ssh/sshd_config`

**Let’s see what steps you can take to secure your SSH server.**

1. Disable empty passwords `PermitEmptyPasswords no`
2. Change default SSH ports `Port 2345`
3. Disable root login via SSH `PermitRootLogin no`
4. Configure idle timeout interval `ClientAliveInterval 300`
5. Disable ssh protocol 1 `Protocol 2`
6. Allow SSH access to selected users only `AllowUsers User1 User2`
7. Disable password based SSH login


## Steps 4: Allowing SSH through the firewall
Ubuntu comes with a firewall utility called UFW (UncomplicatedFirewall) which is an interface for iptables that in turn manages the network’s rules. If the firewall is active, it may prevent the connection to your SSH Server.
To configure UFW so that it allows the wanted access, you need to run the following command.

`sudo ufw allow from any to any port 2222 proto tcp`

After making all the changes in the main configuration file, save them and close the editor. Restart the service to make the changes take effect.

`sudo systemctl restart ssh`

## Steps 5: Connecting to the remote system from your local machine
Your local Linux system should already have an SSH client installed. If not, you may always install it using the following command on Ubuntu.

`sudo apt install openssh-client`

To connect to your Ubuntu system you need to know the IP address of the computer and use the ssh command.

`ssh username@IPaddress `\
`ssh aorko@192.168.0.200`

`ssh username@IPaddress -p portnumber`\
`ssh aorko@192.168.0.200 -p 22`

## Steps 6: Enable,Disable or Status check
Your commands to manage the SSH service are correct, but the service command is being used alongside systemctl. It's preferable to stick with one of them for consistency. Since Ubuntu 22.04 uses systemd, it's recommended to use systemctl for managing services.
```bash
sudo systemctl status ssh
sudo systemctl stop ssh
sudo systemctl start ssh
sudo systemctl enable ssh
sudo systemctl disable ssh
```

[References](https://github.com/nasirnjs/LinuxOpsHub/edit/main/2-configuring_SSH.md)

