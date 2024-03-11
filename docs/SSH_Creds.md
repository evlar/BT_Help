# Setting Up SSH Credentials on a VPS

This guide outlines the steps for setting up SSH credentials on a Virtual Private Server (VPS). These steps are essential for securing SSH access and include handling changed passwords or resets, troubleshooting common problems, and resetting your server if necessary.

## Setting Up SSH for the First Time

If you're setting up SSH for the first time on your VPS, follow these concise steps to generate a new SSH key pair, transfer your public key to the server, and ensure secure SSH access.

1. **Generate SSH Key Pair:**

   On your local machine, generate a new SSH key pair with:

   ```bash
   ssh-keygen -t rsa -b 4096
   ```

   Follow the prompts to specify the file location and passphrase (optional).

2. **Copy Public Key to Server:**

   Transfer your public key to the server's `~/.ssh/authorized_keys`:

   ```bash
   ssh-copy-id user@your.server.ip.address
   ```

   Replace `user` with your server's username (e.g., `root`) and `your.server.ip.address` with your server's IP address.

3. **Login to Your Server:**

   Now, you can log into your server without a password:

   ```bash
   ssh user@your.server.ip.address
   ```

4. **(Optional) Disable Password Authentication:**

   To enhance security, disable password authentication on your server. Edit the SSH configuration file:

   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

   Find the line `#PasswordAuthentication yes` and change it to `PasswordAuthentication no`. Save and close the file.

5. **Restart SSH Service:**

   Apply the changes by restarting the SSH service:

   ```bash
   sudo systemctl restart ssh
   ```

By completing these steps, you've successfully set up SSH for the first time, enhancing the security of your server access.

## Handling Changed Passwords or Resets

### Removing the Old Host Key Entry

If you've changed your VPS password or reset your server, the first step is to remove the old host key entry from your local machine. Open your terminal and execute the following command:

```bash
ssh-keygen -f "/home/yourusername/.ssh/known_hosts" -R "your.server.ip.address"
```

Replace `/home/yourusername/.ssh/known_hosts` with your actual path and `your.server.ip.address` with your VPS's IP address.

### Scanning for the New Host Key

Next, scan for the new host key and add it to your known hosts:

```bash
ssh-keyscan your.server.ip.address | tee -a ~/.ssh/known_hosts
```

Replace `your.server.ip.address` with your server's IP address.

### Logging In

To log into your server, use:

```bash
ssh root@your.server.ip.address
```

Replace `your.server.ip.address` with your server's IP address.

## Troubleshooting Common Problems

If you encounter issues, follow these steps to verify your SSH key pair:

1. **Locate Your Private Key (`id_rsa`):**
   
   Ensure your private key is in the `~/.ssh` directory:

   ```bash
   ls -l ~/.ssh
   ```

   Confirm that `id_rsa` is listed.

2. **Check Private Key Permissions:**
   
   Correct permissions are crucial. Set them with:

   ```bash
   chmod 600 ~/.ssh/id_rsa
   ```

3. **Check Your Public Key:**
   
   Display your public key to ensure it matches the server's:

   ```bash
   cat ~/.ssh/id_rsa.pub
   ```

4. **SSH to the Remote Server:**
   
   Use your private key for authentication:

   ```bash
   ssh -i ~/.ssh/id_rsa root@your.server.ip.address
   ```

Replace `your.server.ip.address` with your server's actual IP address.

## Resetting Server: Next Steps

If you've reset your server and need to set up SSH access again, follow these steps:

1. **Log into Your Server:**

   ```bash
   ssh root@your.server.ip.address
   ```

2. **Create the `.ssh` Directory and `authorized_keys` File:**

   ```bash
   mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys
   ```

3. **Set Permissions:**

   Ensure the `.ssh` directory and `authorized_keys` file have the correct permissions:

   ```bash
   chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys
   ```

4. **Copy Your Local Public Key to the Remote Server:**

   Exit your current SSH session and run:

   ```bash
   ssh-copy-id root@your.server.ip.address
   ```

5. **Restart the SSH Service:**

   Log back into your server and restart the SSH service:

   ```bash
   ssh root@your.server.ip.address
   sudo systemctl restart ssh
   exit
   ```

6. **Test Your SSH Connection:**

   Finally, test your SSH connection without being prompted for a password:

   ```bash
   ssh -i ~/.ssh/id_rsa root@your.server.ip.address
   ```

Replace `your.server.ip.address` with your server's actual IP address. Now you should have a securely configured SSH access to your VPS.
