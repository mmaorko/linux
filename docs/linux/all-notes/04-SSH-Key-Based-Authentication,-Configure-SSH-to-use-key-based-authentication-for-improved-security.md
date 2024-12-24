# How To Configure SSH Key-Based Authentication on a Linux Server and custom host

 **authentication methods**
SSH (Secure Shell) supports several authentication methods to verify the identity of the user and ensure secure communication between the client and the server.

Here’s a breakdown of how **SSH key-based authentication** works:
SSH support two authentication method 

 - password authentication
 - public key authenticaiton

***Password authentication*** in SSH (Secure Shell) is a method of verifying a user's identity when they attempt to connect to a remote server. It requires the user to provide a password associated with their account on the remote machine in order to gain access.
***Public Key Authentication*** is a method of authenticating to an SSH server without the need to enter a password each time. Instead of using a password to prove your identity, you use a pair of cryptographic keys: a ***private key*** (kept secret) and a ***public key*** (shared with the server). This method is more secure than password-based authentication and is commonly used for automating secure logins and enhancing security.


**Here's how it works:**

1.  **Key Generation**: A public key and a private key are first created on your local computer. The public key is freely shared, while the private key is kept private on your local computer.
    
2.  **Public Key Placement**: The public key is placed on the server that you want to connect to. This is typically done by appending the contents of your public key file to the  `~/.ssh/authorized_keys`  file on the server
    
3.  **Authentication**: Your public key is sent to the server by your SSH client when you try to connect. The server verifies whether the `authorized_keys` file has this public key.It generates a challenge using the public key and sends it to your client if it detects a matching public key.
    
4.  **Private Key Usage**: Your SSH client then uses your private key to decrypt the challenge and sends the decrypted response back to the server. If the server successfully decrypts the response using the corresponding public key, you are granted access.

#### Best Practices for Public Key Authentication:
it is crucial to follow best practices to ensure that your SSH keys remain secure and your system is protected. Here are some of the best practices for SSH key-based authentication:
### 1. **Use Strong SSH Key Sizes**
-   **RSA Key Size**: When generating RSA keys, always use a key size of at least 2048 bits. 4096 bits is preferred for stronger security.
-   **Ed25519**: For even better security and performance, consider using Ed25519 keys, which provide a higher level of security with shorter key sizes (256 bits). Ed25519 is designed to be more secure and faster than RSA.

### 2. **Use Passphrases for Your Private Keys**
-   **Encryption**: Encrypt your private keys with a strong passphrase. This adds an extra layer of security in case your private key is compromised.
-   **Security of the Passphrase**: Use a strong, unique passphrase (not easily guessable), and store it securely (for example, in a password manager).
-   **SSH Agent**: If you frequently use SSH, you can use an SSH agent to cache your passphrase in memory, so you don't need to enter it each time. For example, use `ssh-agent` or a similar tool to manage your private key passphrases securely.
- 
### 3. **Disable Root Login**
-   **Root Access**: For additional security, disable root login via SSH and use a regular user account with `sudo` privileges. This helps to prevent attackers from directly trying to brute-force the root account.

### 4. **Limit SSH Access by IP**
-   **Firewall Rules**: Restrict SSH access to trusted IP addresses or address ranges using firewall rules (such as `iptables` or `ufw` on Linux).
-   **Fail2Ban**: Use intrusion detection tools like **Fail2Ban** to block IPs that make repeated, failed login attempts, protecting the server from brute-force attacks.

***ssh-authentication Architecture***
![ssh-authentication Architecture](https://i.ibb.co.com/kHWrPvC/ssh-initiate-connection.png)

### **Step 1: Generate an SSH Key Pair**

1.  **Open Terminal:** On your local machine, open a terminal. Generate Key Pair and run the following command:

`ssh-keygen -t rsa -b 4096`
  ### **Step 2: Copy the Public Key to the Server**
1.  **Use** `ssh-copy-id` **Command:**\
`ssh-copy-id username@server_ip`

### step 3: Log in to your server:
first of all test ssh connection

`ssh username@server_ip`
### Step 4: Optional - Create SSH Config File
To simplify connections, you can create an SSH config file (~/.ssh/config) on your local machine. Edit the file with a text editor. 

`vim ~/.ssh/config`

Add the following lines, replacing "hostname" with your remote host's address and "key" with the path to your private key.


```
Host myhost
  HostName username/server_ip
  User username
  Port 1234
  IdentityFile ~/.ssh/key

```
then finally,
**Connect Using SSH Key** On your local machine, connect to the server:

`ssh username@server_ip`
