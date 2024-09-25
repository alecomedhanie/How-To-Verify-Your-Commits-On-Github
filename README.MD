To verify your commits on GitHub, you can sign your commits with **GPG (GNU Privacy Guard)** keys. This ensures that your commits are marked as "verified" and proves that they come from you. Here's a step-by-step guide to set up GPG signing and verify your commits on GitHub:

### 1. **Install GPG**
First, you need to install GPG if it's not already installed on your system:

- **macOS**:
  ```bash
  brew install gnupg
  ```
- **Ubuntu/Debian**:
  ```bash
  sudo apt install gnupg
  ```
- **Windows**:
  Download and install from [GPG for Windows](https://gpg4win.org/).

### 2. **Generate a GPG Key**
Once GPG is installed, you can generate a new GPG key:

1. Open a terminal and run:
   ```bash
   gpg --full-generate-key
   ```

2. Follow the prompts:
   - Choose `RSA and RSA` (option 1).
   - Enter a key size (recommend 4096 bits).
   - Set the key to never expire or set an expiration date.
   - Enter your real name and email address (this should match the email you use on GitHub).
   - Set a secure passphrase.

3. After the key is generated, list your GPG keys:
   ```bash
   gpg --list-secret-keys --keyid-format LONG
   ```

4. Copy the **GPG key ID**:
   The key ID will look something like this:
   ```
   /Users/youruser/.gnupg/secring.gpg
   ------------------------------------
   sec   4096R/<YOUR_KEY_ID> 2024-09-17
   uid                  Your Name <youremail@example.com>
   ssb   4096R/XXXXXXXX 2024-09-17
   ```

   Copy the `<YOUR_KEY_ID>` (the part after `sec`).

### 3. **Add the GPG Key to GitHub**

1. Export your GPG public key:
   ```bash
   gpg --armor --export <YOUR_KEY_ID>
   ```

2. Copy the entire output of the command (this is your public key).

3. Go to your GitHub account settings:
   - Navigate to **Settings > SSH and GPG keys**.
   - Click **New GPG key**.
   - Paste your GPG public key and click **Add GPG key**.

### 4. **Configure Git to Sign Commits by Default**

1. Set Git to use your GPG key by running:
   ```bash
   git config --global user.signingkey <YOUR_KEY_ID>
   ```

2. Enable commit signing globally by running:
   ```bash
   git config --global commit.gpgSign true
   ```

### 5. **Sign a Commit**

Now that everything is set up, every commit you make will be signed. If you want to manually sign a commit, you can use the `-S` option when committing:

```bash
git commit -S -m "Your commit message"
```

Git will prompt you for the passphrase for your GPG key if necessary.

### 6. **Verify Commit on GitHub**

1. Push your signed commit to GitHub:
   ```bash
   git push origin main
   ```

2. Go to your repository on GitHub and navigate to the commits section. You should see a "Verified" badge next to your commit, which means the commit was signed and verified correctly.

### 7. **Check Verification on GitHub**

- **Green "Verified" badge**: This means your commit was signed and verified successfully.
- **Yellow "Unverified" badge**: This means the commit was signed, but GitHub could not verify it (often due to mismatched email addresses or GPG keys).
  
---

### Troubleshooting

- **GPG Key Doesn't Match GitHub Email**: Ensure the email you use for your GPG key matches the email on your GitHub account.
- **GPG Not Working on macOS with Git**: You may need to tell Git where your `gpg` is located:
  ```bash
  git config --global gpg.program $(which gpg)
  ```

Now, your commits should be signed and verified! Let me know if you have any issues with setting this up.