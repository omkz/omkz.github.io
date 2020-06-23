---
published: true
title: Add a new user on Amazon EC2 Ubuntu 12.04 instance
layout: post
categories: linux
tags: [linux, aws,ec2]
---

Yea that's right Ubuntu 12.04, that's not the wrong title. The following are the steps to create a user on Ubuntu 12.04.

Create a new user named `deploy` with a home directory of /opt/deploy:

```
useradd -m -d /opt/deploy deploy
or
adduser deploy --home /opt/deploy
```

Create the deploy user and add them to the sudo group.
```
useradd deploy sudo
or
adduser deploy sudo
```
Create password for user `deploy`:
```
passwd deploy
```
Switch to the new account so that the directory and file that you create will have the proper ownership.
```
sudo su - deploy
```
Create a `.ssh` directory in the `deploy` home directory and change its file permissions to 700 (only the owner can read, write, or open the directory).
```
mkdir .ssh
chmod 700 .ssh
```

Create a file named `authorized_keys` in the `.ssh` directory and change its file permissions to 600 (only the owner can read or write to the file).
```
touch .ssh/authorized_keys
chmod 600 .ssh/authorized_keys
```
In the `localhost` Retrieve the public key from the key pair:
```
 ssh-keygen -y -f /path_to_key_pair/key-pair-name.pem
 ```
The command returns the public key, as shown in the following example:
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQClKsfkNkuSevGj3eYhCe53pcjqP3maAhDFcvBS7O6Vhz2ItxCih+PnDSUaw+WNQn/mZphTk/a/gU8jEzoOWbkM4yxyb/wB96xbiFveSFJuOp/d6RJhJOI0iBXrlsLnBItntckiJ7FbtxJMXLvvwJryDUilBMTjYtwB+QhYXUMOzce5Pjz5/i8SeJtjnV3iAoG/cQk+0FzZqaeJAAHco+CY/5WrUBkrHmFJr6HcXkvJdWPkYQS3xqC0+FmUZofz221CBt5IMucxXPkX4rWi+z7wB3RbBQoQzd8v7yeb7OzlPnWOyN0qFU0XA246RA8QFYiCNYwI3f05p6KLxEXAMPLE
```

In the `server`, Open the `authorized_keys` file using your favorite text editor (such as vim or nano). And then Paste the public key that you retrieved above.

```
nano .ssh/authorized_keys
```

Add bash autocompletion if needed:
```
sudo -u deploy chsh -s /bin/bash
cp /etc/skel/.bashrc /opt/deploy
```






 