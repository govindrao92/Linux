# Setting up SSH Keys for GitHub

If you frequently interact with GitHub repositories, using SSH keys allows you to authenticate with GitHub without typing your username and password every time. Here's how to set it up.

## Steps to Generate and Use SSH Keys with GitHub

### Step 1: Generate a New SSH Key Pair

To generate an SSH key pair on your local machine:

1. Open a terminal and enter the following command:

    ```bash
    ssh-keygen -t ed25519 -C "your_email@example.com"
    ```

    If you're using an older system that doesn't support the `ed25519` algorithm, use the `rsa` option:

    ```bash
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    ```

2. When prompted, choose a file location to save the key pair (press Enter to accept the default path: `~/.ssh/id_ed25519` or `~/.ssh/id_rsa`).

3. When prompted for a passphrase, you can either enter one for added security or leave it blank for easier access.

### Step 2: Add Your SSH Key to the SSH Agent

1. Start the SSH agent in the background:

    ```bash
    eval "$(ssh-agent -s)"
    ```

2. Add your SSH private key to the SSH agent:

    ```bash
    ssh-add ~/.ssh/id_ed25519
    ```

    Or if you used RSA:

    ```bash
    ssh-add ~/.ssh/id_rsa
    ```

### Step 3: Add Your SSH Public Key to GitHub

1. Copy your SSH public key to the clipboard:

    ```bash
    cat ~/.ssh/id_ed25519.pub
    ```

    Or for RSA:

    ```bash
    cat ~/.ssh/id_rsa.pub
    ```

    Alternatively, use the following commands:
    - macOS:
      ```bash
      pbcopy < ~/.ssh/id_ed25519.pub
      ```
    - Linux:
      ```bash
      xclip -sel clip < ~/.ssh/id_ed25519.pub
      ```

2. Go to GitHub and log in.

3. In the upper-right corner of any page, click your profile photo, then click **Settings**.

4. In the user settings sidebar, click **SSH and GPG keys**.

5. Click **New SSH key** or **Add SSH key**.

6. In the "Title" field, add a descriptive label for the new key, like "My Laptop Key".

7. Paste your public key into the "Key" field.

8. Click **Add SSH key**.

### Step 4: Test the SSH Connection to GitHub

To confirm that your SSH key has been added correctly:

1. In your terminal, run:

    ```bash
    ssh -T git@github.com
    ```

2. You should see a message like this:

    ```
    Hi username! You've successfully authenticated, but GitHub does not provide shell access.
    ```

Now you can use SSH to interact with your GitHub repositories without typing your username and password.

### Optional: Disable Password Login for SSH (Advanced)

To enforce SSH key-based logins only (without passwords) on a remote server:

1. Edit the SSH configuration on your remote server:

    ```bash
    sudo nano /etc/ssh/sshd_config
    ```

2. Find the line that says `PasswordAuthentication yes` and change it to:

    ```bash
    PasswordAuthentication no
    ```

3. Restart the SSH service:

    ```bash
    sudo systemctl restart ssh
    ```

> **Note:** This step is not necessary for GitHub, as GitHub only uses SSH keys for authentication.

---

By following these steps, you can securely connect to GitHub using SSH.



