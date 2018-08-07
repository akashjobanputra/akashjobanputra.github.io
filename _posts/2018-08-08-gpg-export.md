---
layout: post
title: "move your key"
description: "Move your private key to another system"
tags: [gpg, git]
---

<!-- In my previous blogs, I had shown how and why you should sign your git commits. And as mentioned in that, I had made my keys using gpg which was stored in local keystore of the machine I was working on. Recently, I was using a different machine and had to make commits and while doing that I realized I don't have my keys in the current machine. So had to export them from previous machine and import them to the new machine. -->
## Extract Private Key
1. List the keys in the system to copy the ID of your private key  
    `$ gpg --list-secret-keys`
2. Copy the ID of your private key and paste it in below command. This will generate the file containing the private key.  
    `$ gpg --export-secret-keys [private-key-ID] > my_private_key.asc`

## Import Private Key to another machine
1. Copy the private key file to the other machine in any suitable way, using `scp` or by usb storage or anything.  
2. Run `$ gpg --import my_private_key.asc` And your key will get imported.

### Set up the key for signing in the new machine
1. You need to tell git about your signing key, copy the GPG key ID from step 9 above and paste it in
    ```bash
    $ git config --global user.signingkey FAAC90B03A08A733
    ```
