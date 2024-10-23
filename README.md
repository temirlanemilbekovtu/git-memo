# GUIDE TO SOLVE YOUR PROBLEMS

## Navigation

- [Preface](#preface)
- [fatal: Authentication failed](#fatal-authentication-failed)
- [fatal: Something not found](#fatal-something-not-found)
- [Permission denied](#permission-denied)
- [Permission denied (publickey)](#permission-denied-publickey)

## Preface

Hello, silly boy/girl. If you're reading this, it means you've encountered issues with Git, and Mr. Migranov has redirected your problem-solving request to this document. Good for you I know how to resolve your problem. First find your issue on the [navigation section](#navigation) and then follow described instructions.

## fatal: Authentication failed


## fatal: Something not found


## Permission denied

If you're facing a "403 Forbidden" error while trying to push or pull from a Git repository, it’s usually due to incorrect credentials or access issues.

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
    If it shows an HTTPS URL (e.g., https://github.com/...), it’s recommended to switch to SSH for better security. To change the remote URL to SSH, run:
    ``` sh
    git remote set-url origin git@github.com:USERNAME/REPO.git
    ```
    Replace USERNAME and REPO with your actual GitHub username and repository name.

4.  **Set up your SSH key**  
    Make sure your SSH key is added to your GitHub account. Refer to the steps in the [section below](#permission-denied-publickey) to generate and add an SSH key if you haven’t done so.

5.  **Clear cached credentials (if using HTTPS)**
    If you're using HTTPS and previously entered wrong credentials, clear the cached credentials:
    ``` sh
    git credential-cache exit
    ```
    Then try to push or pull again. Git will prompt you for credentials, where you can enter the correct ones.

6.  **Retry your Git command**
    Once you've verified access and set up your credentials, run the Git command again to see if the issue is resolved.

## Permission denied (publickey)

If you're encountering the "Permission denied (publickey)" error, it's likely due to an improper SSH key setup.

### Steps to resolve the issue:

1.  **Generate an SSH keypair**  
    If you don't have an SSH key, generate one using the following command in your terminal:  
    ``` sh
    ssh-keygen -t rsa -b 4096
    ```
    You'll be prompted to specify a file path for saving the key. Press enter to use the default location. Next, you'll be asked to enter a passphrase. Remember it if you choose one. Your SSH keypair (private and public keys) will now be generated and stored in the path you specified.  

2.  **Add your SSH to GitHub**
    - Log in to your GitHub account and go to `Settings` > `SSH and GPG keys`.
    - Click the `New SSH key` button.
    - In the `Key` field, paste the contents of your public key file.
    - Finish by clicking `Add SSH key` button.
    Now try to run the command you, which you met the issue with.

3. **Retry your Git command**  
    Now, try the command again that initially gave you the "Permission denied" error.
