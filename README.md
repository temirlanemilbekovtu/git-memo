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


## Permission denied (publickey)
If you're encountering the "Permission denied (publickey)" error, it's likely due to an improper SSH key setup.
### Steps to resolve this issue:
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
3. **Retry your command**  
    Now, try the command again that initially gave you the "Permission denied" error.