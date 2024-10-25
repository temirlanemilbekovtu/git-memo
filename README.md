# GUIDE TO SOLVE YOUR PROBLEMS

[**RUSSIAN VERSION**](README_RU.md)

##  Navigation

-   [Preface](#preface)
-   [How to open terminal](#how-to-open-terminal)
-   [SSH keypair generating](#ssh-keypair-generating)
-   [Port 22](#port-22)
-   [Permission denied](#permission-denied)
-   [Permission denied (publickey)](#permission-denied-publickey)
-   [Fatal: Authentication failed](#fatal-authentication-failed)

##  Preface

Hello, silly boy/girl. If you're reading this, it means you've encountered issues with Git, and Mr. Migranov has redirected your problem-solving request to this document.  
Good for you I know how to resolve your problem. First find your issue on the [navigation section](#navigation) and then follow described instructions.

## How to open terminal

### Windows

There is no terminal in Windows, but there is a console. But we will call terminal anyway. In order to open a terminal window in Windows follow the step below:

1.  Press `Win+R`, type `cmd` and press `Enter`.

### Linux

To open a terminal window in a Linux distribution follow the instruction:

1.  Press `Ctrl+Alt+T` or `Shift+Ctrl+T`.

2.  If it doesn't work, then try to find a terminal app via a search engine.

3.  If you don't understand the previous step, or it doesn't work, then use `Ctrl+Alt+F2` (or F3-F6). It will open the console line interface. To get back to GUI use `Ctrl+Alt+F1` (of F7).

## SSH keypair generating

If you don't have an SSH keypair yet, you need to generate one to authenticate with remote repositories over SSH.

### Steps to generate an SSH keypair

1.  **Generate the SSH keypair**  
    Run the following command in a terminal window to generate a new SSH keypair:
    ``` sh
    ssh-keygen -t rsa -b 4096
    ```
    - `-t rsa` specifies the type of key (RSA).
    - `-b 4096` sets the key length to 4096 bits for better security.

2.  **Choose a location for the key**  
    You'll be prompted to specify a file to save the key. Press `Enter` to accept the default location (`~/.ssh/id_rsa`).

3.  **Set a passphrase (optional)**  
    You'll be asked to enter a passphrase for your key. This adds an extra layer of security. You can press `Enter` to skip this, but using a passphrase is recommended.

4.  **Add the SSH key to the agent**  
    Once your key is generated, add it to your SSH agent:
    ``` sh
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_rsa
    ```
    Replace `id_rsa` with the name of your private key file, if it's different.

5.  **Add your public key to GitHub**  
    Copy the public key to your clipboard:
    ``` sh
    cat ~/.ssh/id_rsa.pub
    ```
    Then go to GitHub's `Settings` > `SSH and GPG keys`, click `New SSH key`, and paste your key.

6.  **Test your connection**  
    Verify that everything is working by running:
    ``` sh
    ssh -T git@github.com
    ```
    You should see a success message confirming the connection.

##  Port 22

This error usually occurs due to an incorrect or malformed remote repository URL in your Git configuration.

### Steps to resolve

1.  **Check arguments correctness**  
    Ensure arguments you specified for your git command are proper.

2.  **Check your remote URL**  
    Run the following command in your terminal to check the current remote URL:
    ``` sh
    git remote -v
    ```
    Ensure that the URL is correct. If not, update it by running:
    ``` sh
    git remote set-url origin CORRECT_URL
    ```
    Replace `CORRECT_URL` with the correct repository URL (either HTTPS or SSH).

3.  **Verify internet connection**  
    Ensure you have an active internet connection, as Git might return the error if the network is down.

4.  **Check repository access**  
    If you're using HTTPS, ensure you have the correct credentials to access the repository. For SSH, make sure your SSH keys are properly configured and added to your GitHub.

5.  **Retry your git command**  
    After fixing the URL or credentials, retry the Git command that caused the error.

##  Permission denied

If you're facing a "403 Forbidden" error while trying to push or pull from a Git repository, it's usually due to incorrect credentials or access issues.

### Steps to resolve the issue:

1.  **Resign oneself**  
    If you wanna mess up somebody's repo, but you ain't got collaborator access, it ain't gonna work, boy/girl.

2.  **Check your repository access**  
    Ensure that you have the correct permissions for the repository. If it's private, confirm that you are either the owner or have been granted collaborator access.

3.  **Verify your remote URL**  
    Run the following command to check the remote URL of the repository:
    ``` sh
    git remote -v
    ```
    If it shows an HTTPS URL (e.g., https://github.com/...), it's recommended to switch to SSH for better security. To change the remote URL to SSH, run:
    ``` sh
    git remote set-url origin git@github.com:USERNAME/REPO.git
    ```
    Replace USERNAME and REPO with your actual GitHub username and repository name.

4.  **Set up your SSH key**  
    Make sure your SSH key is added to your GitHub account. Refer to the steps in the [section above](#ssh-keypair-generating) to generate and add an SSH key if you haven't done so.

5.  **Clear cached credentials (if using HTTPS)**  
    If you're using HTTPS and previously entered wrong credentials, clear the cached credentials:
    ``` sh
    git credential-cache exit
    ```
    Then try to push or pull again. Git will prompt you for credentials, where you can enter the correct ones.

6.  **Retry your Git command**  
    Once you've verified access and set up your credentials, run the Git command again to see if the issue is resolved.

##  Permission denied (public key)

This error occurs when Git cannot authenticate your SSH key with the remote repository.

### Steps to resolve

1.  **Check if SSH key is added**  
    Ensure that your SSH key is added to your SSH agent. Run the following command to check:
    ``` sh
    ssh-add -l
    ```
    If no keys are listed, you may need to add your key with:
    ``` sh
    ssh-add ~/.ssh/id_rsa
    ```
    Replace `id_rsa` with the name of your private key file, if it's different.

2.  **Add your SSH key to GitHub**  
    If your SSH key isn't added to your GitHub account, follow these steps:
    - Go to `Settings` > `SSH and GPG keys` on GitHub.
    - Click `New SSH key`, paste your public key (usually found in `~/.ssh/id_rsa.pub`), and save it.

3.  **Verify your SSH connection**  
    Test your connection to GitHub using:
    ``` sh
    ssh -T git@github.com
    ```
    If authentication succeeds, you'll see a message like "Hi USERNAME! You've successfully authenticated."

4.  **Ensure SSH config is correct**  
    Check your SSH config file (`~/.ssh/config`) to ensure it has the correct settings:
    ``` config
    Host github.com
        User git
        Hostname github.com
        IdentityFile ~/.ssh/id_rsa
    ```
    Modify the `IdentityFile` path if you're using a different SSH key.

5.  **Retry your Git command**  
    After ensuring everything is properly configured, try running your Git command again.

## Fatal: Authentication failed
    
This error typically occurs when Git cannot authenticate your credentials for a remote repository.

### Steps to resolve

1.  **Check your Git remote URL**  
    Make sure you're using the correct repository URL (preferably an SSH URL). Run the following command to verify:
    ``` sh
    git remote -v
    ```
    If you're using an HTTPS URL and want to switch to SSH, update it with:
    ``` sh
    git remote set-url origin git@github.com:USERNAME/REPO.git
    ```
    Replace USERNAME and REPO with your actual GitHub username and repository name.

2.  **Update your credentials**  
    If you're using HTTPS and don't want to switch to SSH, ensure that your credentials are up to date:  
    - For GitHub, use a Personal Access Token (PAT) instead of a password, cause password doesn't work anymore. You can generate a token by going to `Settings` > `Developer settings` > `Personal access tokens` on GitHub.  
    - Replace your old password with this token when prompted during Git operations.

3.  **Configure SSH keys (if switching to SSH)**  
    If you switch to SSH and haven't set up your SSH keys yet, follow the steps described in [this section](#ssh-keypair-generating).
    
4.  **Retry your Git command**  
    After updating your credentials, try running your Git command again.
