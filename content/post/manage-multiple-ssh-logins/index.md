---
title: "Manage Multiple SSH Logins"
description: "Using a spreadsheet does not always make you clever"
date: "2018-09-13"
tags: ["tooling", "bash", "ssh"]
---

It can be quite cumbersome when you have a lot of remote servers to log into. If they support SSH access or if you can configure them to do so, managing access to multiple servers can be pleasantly manageable.

What most programmers don't seem to know is that SSH can use a configuration file in `~/.ssh/config` to create an alias of sorts for SSH hosts. If you use aliases in Bash then you can think of this as an alias for creating an SSH connection to a server. 

```bash
# Without config
ssh -i ~/.ssh/linode01.id_rsa czar.pino@120.111.122.123

# With config
ssh cp.linode01
```

By using the `~/.ssh/config` file, it no longer becomes necessary to provide all of the connection parameters every time you want to connect. All information needed to connect to a host can just be defined in a host entry inside the config file.

```
Host cp.linode01
    Hostname 120.111.122.123
    User czar.pino
    IdentityFile ~/.ssh/linode01.id_rsa
```

Another side benefit to this is that you also automatically have a document of all SSH servers you can connect to. No need to maintain an easily outdated spreadsheet which has to be updated separately.

```
Host cp.linode01
    Hostname 120.111.122.123
    User czar.pino
    IdentityFile ~/.ssh/linode01.id_rsa

Host cp.linode02
    Hostname 120.111.122.124
    User czar.pino
    IdentityFile ~/.ssh/linode02.id_rsa

Host cp.ec2-01
    Hostname 121.111.122.123
    User ec2-user
    IdentityFile ~/.ssh/ec2-01.id_rsa

Host cp.ec2-02
    Hostname 121.111.122.124
    User ec2-user
    IdentityFile ~/.ssh/ec2-02.id_rsa
```


