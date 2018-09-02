---
title: "How to tell Git which SSH key to use"
description: "Or, how to push using multiple GitHub accounts"
date: "2018-09-10"
tags: ["git", "ssh", "tooling", "bash", "github"]
---

# How to tell Git which SSH key to use

It is not possible to tell Git which SSH credentials to use — strictly speaking. But you can use SSH config to effectively achieve the same result.

Suppose you have a private key `~/.ssh/special_id_rsa` and you are trying to clone the repository `git@github.com:username/reponame.git`. You would need to add a new host entry to your SSH config that uses the desired private key.

```bash
# ~/.ssh/config  
Host your.hostname.com  
    Hostname github.com  
    User git  
    IdentityFile ~/.ssh/`special_id_rsa`
```

If the SSH config file `~/.ssh/config` does not exist, simply create it and add the host info. You then clone the repository by replacing the repo url domain with the host defined in the SSH config.

```bash
git clone git@your.hostname.com:username/reponame.git
```

After successful clone,`git fetch` and `git commit` will automatically use the `special_id_rsa` private key to connect to the Git server.

For already existing repositories however, you will additionally need to modify the Git config file `.git/config` inside the project. The url of remote “origin” must be changed to the host defined in `~/.ssh/config`.

```bash
# .git/config  
[remote "origin"]  
    url = git@your.hostname.com:username/reponame.git
```

Now you can “tell” Git which SSH credentials to use through SSH config.

> _This article first appeared on [Medium](https://medium.com/@czarpino/how-to-tell-git-which-ssh-key-to-use-c8574fb243fd) last 9-10-2017_