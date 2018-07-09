---
layout: post
title: "git signing"
description: "Setup signing for git commits"
tags: [git]
---

If you don't know why you should sign your git commits, <a href="/posts/why-git-signing" target="_blank">check this out</a>. In gist, signing the commits verifies that it is indeed from the author mentioned in the commit details.  
For signing commits if you don't have one, we first need to generate a key. I use my key generated from <a href="https://www.keybase.io" target="_blank">Keybase.io</a> for personal email, and had generated key using GPG for work account. You can use any one of them for generating the keys.  
## For Generating Keys using GPG and adding it to GitHub:
1. Hit the below command in terminal to start key generation.  
    `$ gpg --full-gen-key`
2. At the prompt, either select the kind of the key you want, or press Enter to accept the default `RSA and RSA`.
3. At the key size prompt enter the max value, `4096`. And hit Enter.
4. Enter the time for how long key should be valid. Press `Enter` to specify the default selection `0`, indicating that the key won't expire.
5. Verify that selections.
6. Enter your user ID information. Make sure the email id you enter here is one of the verified email in your github account. Key will be used to verify commits against that email.
7. Enter a passphrase.
8. Use the below command to list GPG keys for which we have Public and Private keys. Private keys are required to sign commits and tags
    `$ gpg --list-secret-keys --keyid-format LONG`
9. From the list of GPG keys, copy the GPG key ID you'd like to use. In this example, the GPG key ID is `FAAC90B03A08A733`:
    ```bash
    $ gpg --list-secret-keys --keyid-format LONG
    /home/akashj/.gnupg/pubring.kbx
    -------------------------------
    sec   rsa3072/FAAC90B03A08A733 2018-07-07 [SC] [expires: 2018-07-08]
          7B46C11B914D1B551E3662C8FAAC90B03A08A733
    uid                 [ultimate] XYZPQR
    ssb   rsa3072/5DE09A35133ECF55 2018-07-07 [E] [expires: 2018-07-08]
    ```
10. Paste your key ID instead of `FAAC90B03A08A733` in
    ```bash
    $ gpg --armor --export FAAC90B03A08A733
    ```
11. Copy your GPG key, starting with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ends with `-----END PGP PUBLIC KEY BLOCK-----`.
12. Go to SSH and GPG keys in Github Settings and click on New Key button
13. Paste the key copied on step 11 and click on Add GPG Key button.
14. Enter your Github password to confirm.

## Using the generated key to sign commits:
1. You need to tell git about your signing key, copy the GPG key ID from step 9 above and paste it in
    ```bash
    git config --global user.signingkey FAAC90B03A08A733
    ```
2. Now onwards, when committing changes in your local branch, add the -S flag to the git commit command:
    ```bash
    git commit -S -m "your commit message"
    ```
3. It will ask passphrase for signing, provide the passphrase you entered while generating your key (in step 7 above).
4. After completing your commits, enter `git push` to push your commits to your remote repository.
5. You can now go to Github and check the verified badge on your commits, the badge won't appear on previous commits as they were not signed until now.

### Tips:
1. To sign all commits by default in any local repository on your computer, run `git config --global commit.gpgsign true`.
Doing this you won't need to add `-S` flag everytime you commit. A normal `git commit -m "your message"` will by default sign your commits, you'll just have to enter the passphrase.
2. If you use VSCode for creating commits and remote synchronization too, and you want to sign commits using VSCode too. Enter the below command in terminal.
    ```bash
    git config --global gpg.program $(which gpg2)
    ```
